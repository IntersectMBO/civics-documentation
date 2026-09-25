# Resources

This is the place to start if you are thinking about joining the Constitutional Committee, or simply want to understand what the role actually involves. It gathers, in one page, what the CC does, what the role asks of you, the ways you can hold and secure the credentials the role requires, and where to practise all of it safely before anything is real.

Work through it top to bottom the first time. Come back to the credential and practice sections when you are ready to do the hands-on parts.

> **One thing to internalise before anything else.** Holding a Constitutional Committee seat is a key-management responsibility as much as a governance one. A cold credential that is generated in an online environment is compromised from the moment it is created, and there is no way to undo that. Read the Credentials and key security section carefully, and generate your cold keys offline from the start.

***

### 1. Understand the role

The Constitutional Committee is Cardano's **constitutional court, not a policy body.** Its one job is to judge whether a governance action is consistent with the [Cardano Constitution](https://cap.intersectmbo.org/#/constitution). It does not decide whether an action is a good idea; DReps and the community do that.

Cardano's on-chain governance ([CIP-1694](https://cips.cardano.org/cip/CIP-1694), the Voltaire era) shares power across three bodies:

| Body                                  | Role                                                                   |
| ------------------------------------- | ---------------------------------------------------------------------- |
| **Constitutional Committee (CC)**     | Checks that actions comply with the Constitution.                      |
| **Delegated Representatives (DReps)** | The primary voice of ADA holders on the merits.                        |
| **Stake Pool Operators (SPOs)**       | Vote on specific action types, notably hard forks and some parameters. |

For each governance action, the CC votes **Constitutional, Unconstitutional, or Abstain.** Most action types need a 2/3 threshold of the CC to ratify, so the committee has to reach and record a collective position on the constitutionality of live actions.

**Read these to understand the job:**

* [Cardano governance, the concept](https://developers.cardano.org/docs/developers/curriculum/staking-governance/governance/) (the three bodies, the seven action types, thresholds and lifecycle)
* [CIP-1694](https://cips.cardano.org/cip/CIP-1694), the specification the whole system implements
* [The Cardano Constitution](https://www.cardano.org/governance), which is the text you would be interpreting
* [Constitutional Amendment Process](https://cap.intersectmbo.org/), how that text changes over time

***

### 2. What the role asks of you

Be clear-eyed about the commitment:

* **It is ongoing.** The CC reviews governance actions as they arrive, on their own schedule, throughout the term.
* **It is currently uncompensated.** Future compensation is under discussion but not settled. Take the role because you want to do the work.
* **It is a security responsibility.** You will hold cryptographic credentials that carry a seat on a constitutional body. Losing control of the cold credential has real consequences (see below).
* **It expects transparency.** Members are expected to communicate their decisions and voting rationale to the community.

***

### 3. Credentials and key security

This is the technical heart of the role. Every Constitutional Committee seat is operated through a **two-credential "cold / hot" model.**

* The **cold credential** _is_ the seat. It stays offline and is used for only two things: authorising a hot credential, and resigning the seat.
* The **hot credential** does the day-to-day voting. It is used often, and is designed to be replaceable.

The reason for the split is security. If the **hot** credential is compromised, you simply authorise a new one, which invalidates the old: cheap and recoverable. If the **cold** credential is compromised or lost, there is no easy recovery. The best case is being voted off the committee; the worst case is the whole committee being disbanded by a no-confidence action. That asymmetry is the whole point, and it is why the cold credential must be protected accordingly.

When you take up a seat you register a **cold credential hash**, and you declare its **type**. That type is where the three approaches below differ: a seat can be held by a single key, by a native multi-signature script, or through the Credential Manager. Pick the one that matches who is holding the seat and how much operational machinery you want.

| Approach               | Credential type | Held by                    | Trade-off                                                                        |
| ---------------------- | --------------- | -------------------------- | -------------------------------------------------------------------------------- |
| **Single user**        | Key             | One person                 | Simplest to set up; a single point of failure.                                   |
| **Multisig**           | Native script   | A group, M-of-N signatures | Shared control, no single point of failure; more coordination, no extra tooling. |
| **Credential Manager** | Plutus script   | An organisation, by role   | Most robust and auditable; the most involved to operate.                         |

> **Whichever approach you choose:** generate every cold signing key on an air-gapped, offline machine, and never let a cold signing key touch an internet-connected computer. This is the single most important rule on this page.

The commands below are Conway-era `cardano-cli`. Flags evolve between versions, so confirm against `cardano-cli conway governance committee --help` and the official guides before you rely on them.

#### 3a. Single user (key credential)

One person holds one cold key and one hot key. It is the quickest to stand up, and the right choice for an individual who is confident in their own air-gapped key handling. The cost is that the seat has a single point of failure: if that one cold key is lost or exposed, the only recourse is to resign.

**1. Generate your cold key pair** (do this offline):

```bash
cardano-cli conway governance committee key-gen-cold \
  --cold-verification-key-file cc-cold.vkey \
  --cold-signing-key-file cc-cold.skey
```

**2. Derive your cold credential hash** (this is what you register):

```bash
cardano-cli conway governance committee key-hash \
  --verification-key-file cc-cold.vkey
```

**3. Generate your hot key pair** (this one does the voting):

```bash
cardano-cli conway governance committee key-gen-hot \
  --verification-key-file cc-hot.vkey \
  --signing-key-file cc-hot.skey
```

**4. Authorise the hot key** with your cold key (produces a certificate you submit on-chain once seated):

```bash
cardano-cli conway governance committee create-hot-key-authorization-certificate \
  --cold-verification-key-file cc-cold.vkey \
  --hot-verification-key-file cc-hot.vkey \
  --out-file hot-auth.cert
```

**5. Resign the seat**, if you ever need to (signed by the cold key):

```bash
cardano-cli conway governance committee create-cold-key-resignation-certificate \
  --cold-verification-key-file cc-cold.vkey \
  --out-file resign.cert
```

#### 3b. Multisig (native script credential)

Here the credential is a **native multi-signature script** rather than a single key. Several people each hold their own key, and the script sets the rule for how many of them must sign, for example any 3 of 5. No single person can act alone, and losing one key does not lose the seat. This is the natural fit for a consortium or an organisation that wants shared control without adopting extra tooling. It costs more coordination: every authorisation or resignation needs a quorum of signers.

**1. Each participant generates a cold key pair** (each on their own offline machine, using `key-gen-cold` as above) and shares only their **key hash**:

```bash
cardano-cli conway governance committee key-hash \
  --verification-key-file cc-cold.vkey
```

**2. Assemble the native script** (`cc-cold.script`) from those hashes. For example, "any 3 of these 5 must sign":

```json
{
  "type": "atLeast",
  "required": 3,
  "scripts": [
    { "type": "sig", "keyHash": "<member-1-cold-key-hash>" },
    { "type": "sig", "keyHash": "<member-2-cold-key-hash>" },
    { "type": "sig", "keyHash": "<member-3-cold-key-hash>" },
    { "type": "sig", "keyHash": "<member-4-cold-key-hash>" },
    { "type": "sig", "keyHash": "<member-5-cold-key-hash>" }
  ]
}
```

**3. Hash the script** to get the cold credential hash you register (type: **script**):

```bash
cardano-cli hash script --script-file cc-cold.script
```

**4. Authorise a hot credential** by referencing the script instead of a single key (the hot side can be its own script or a key):

```bash
cardano-cli conway governance committee create-hot-key-authorization-certificate \
  --cold-script-file cc-cold.script \
  --hot-script-file cc-hot.script \
  --out-file hot-auth.cert
```

The resignation certificate takes `--cold-script-file` the same way. In every case, the transaction that publishes the certificate must be signed by the quorum the script requires, and each member signs with their own cold key on their own offline machine.

#### 3c. Credential Manager (Plutus script credential)

The [Credential Manager](https://credential-manager.readthedocs.io/en/latest/) is a purpose-built system from IOG for holding a CC seat as an organisation. The credential is a **Plutus script** backed by an **X.509 certificate chain** and NFTs, and duties are split across defined roles: membership, delegation and voting on the user side, plus a head of security and an orchestrator on the operational side. Two properties make it the most robust option:

* **You can rotate the people in a role without changing the on-chain credential,** so members can come and go while the committee's identity stays fixed.
* **Every signer is tied to a publicly verifiable identity** through the certificate chain, which makes actions auditable.

The trade-off is operational weight: it runs through an orchestrator CLI (Nix, a cloned repository, a Nix shell) and a signing workflow, so it asks for real technical commitment to run well. For an organisation or consortium holding a seat over the long term, that is usually a price worth paying. Start with the [Credential Manager user guide](https://credential-manager.readthedocs.io/en/latest/) and the [cold / hot credential background](https://credential-manager.readthedocs.io/en/latest/background/cc-credentials.html).

#### Applies to all three

* **Air-gap and hardware signing.** Keep every cold signing key off any networked machine.
* **Key derivation standard.** [CIP-0105](https://cips.cardano.org/cip/CIP-0105) defines Conway-era key chains (including committee cold and hot keys) for HD wallets, which is what wallet and tool implementers follow.
* **Verify on-chain.** After any authorisation or resignation, confirm the change landed with `cardano-cli conway query committee-state` (see section 5).

***

### 4. Practise before it is real: SanchoNet

Do not learn this on mainnet. [**SanchoNet**](https://github.com/Hornan7/SanchoNet-Tutorials) is Cardano's dedicated governance testnet, built for exactly this: rehearsing CIP-1694 governance with no real ADA at stake.

* **Get SanchoBucks** in the [SanchoNet Discord](https://discord.com/invite/tHYrxCtdHm).
* **Run a node or go deeper** with the SanchoNet documentation and tutorials.

A good rehearsal, end to end: generate a cold and hot credential (try both the single-key and the native-script route), authorise the hot credential on SanchoNet, find a live governance action, cast a Constitutional / Unconstitutional / Abstain vote as a committee member, and attach a rationale. Once that feels routine, the mainnet version is the same motions with real stakes.

The public **Preview** and **Preprod** testnets are also available for general transaction practice, but SanchoNet is the one built around governance.

***

### 5. How CC members vote, day to day

Once seated, the working loop is: see what is live, form a position, record your vote with a rationale, submit. The queries and the vote command:

**See the current governance state** (committee, constitution, live proposals):

```bash
cardano-cli conway query committee-state      # members, hot-cred auth, expiry, threshold
cardano-cli conway query gov-state            # committee, constitution, params, proposals
cardano-cli conway query proposals --all-proposals
```

**Cast a vote** as a committee member (Yes = Constitutional, No = Unconstitutional):

```bash
cardano-cli conway governance vote create \
  --yes \
  --governance-action-tx-id <TX_ID> \
  --governance-action-index <INDEX> \
  --cc-hot-verification-key-file cc-hot.vkey \
  --out-file vote.json
```

If your seat is held by a script, swap `--cc-hot-verification-key-file` for `--cc-hot-script-file cc-hot.script` and gather the signatures the script requires. You then build, sign (with the hot credential), and submit the transaction that carries the vote. Every vote should carry a **rationale**, published as metadata against a public anchor, so the community can see not just how you voted but why. See the [vote and propose guide](https://developers.cardano.org/docs/developers/curriculum/staking-governance/vote-and-propose/) and [governance operations](https://developers.cardano.org/docs/developers/curriculum/staking-governance/governance-operations/) for the full transaction flow, and [metadata standards](https://cips.cardano.org/cip/CIP-0100) for how rationale anchors are structured.

***

### 6. Tools you will use

| Tool                                                                       | What it is for                                                       |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| [cardano-cli](https://github.com/IntersectMBO/cardano-cli)                 | The command-line path for credential ceremonies and voting.          |
| [Credential Manager](https://credential-manager.readthedocs.io/en/latest/) | Secure, role-based management of CC credentials for an organisation. |
| [The Constitution](https://cap.intersectmbo.org/#/constitution)            | The text you interpret, plus the guardrails.                         |
| [CAP Portal](https://cap.intersectmbo.org/)                                | Where constitutional amendments are proposed and discussed.          |
| Query providers (Blockfrost, Koios, Maestro)                               | Read governance state over HTTP if you are building tooling.         |

***

### 7. Go deeper

**Governance and the Constitution**

* [Cardano governance overview](https://developers.cardano.org/docs/developers/curriculum/staking-governance/governance/) and [governance operations](https://developers.cardano.org/docs/developers/curriculum/staking-governance/governance-operations/) (developer portal)
* [Vote and propose](https://developers.cardano.org/docs/developers/curriculum/staking-governance/vote-and-propose/)
* [CIP-1694](https://cips.cardano.org/cip/CIP-1694), the governance specification
* [The Constitution and participant hub](https://www.cardano.org/governance) (`cardano.org/governance`)

**Credentials and keys**

* [Constitutional Committee cold / hot credential model](https://credential-manager.readthedocs.io/en/latest/background/cc-credentials.html)
* [Credential Manager user guide](https://credential-manager.readthedocs.io/en/latest/)
* [CIP-0105](https://cips.cardano.org/cip/CIP-0105), Conway-era key chains
* [Chang upgrade: public keys and signing](https://cardanofoundation.org/blog/chang-public-keys-signing) (Cardano Foundation)

**Learning the wider landscape**

* [Governance Education resource database](https://docs.google.com/spreadsheets/d/1--LJDJG0uL3gC0S_BJMezso1fBfVAw4nzlyvY3lafrc/edit?usp=sharing), the committee's curated, quality-scored list of community learning material
* Governance Education framework

> Third-party tools and testnets are linked for convenience. Always verify commands against current official documentation, and treat your cold signing key as the most sensitive secret you hold.
