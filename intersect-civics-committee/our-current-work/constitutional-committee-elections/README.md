# Constitutional Committee elections

The Constitutional Committee rules on whether governance actions are constitutional. Its members serve fixed terms, and those terms expire.

Section 3.2 of the Constitution says seats expire. It does not say who has to run an election to refill them. That makes replacement an **unowned function**: if nobody facilitates an election, the Constitutional Committee falls below its minimum size and Cardano's governance stalls.

The Civics Committee has facilitated every Constitutional Committee election so far.

***

### Current process&#x20;

An election has two halves, and both must succeed.

**1. The off-chain election** selects candidates. Registration, credential verification, campaigning, then a DRep vote on Intersect's Hydra-based platform, built on Ekklesia. Results are independently audited before publication. Platform documentation: [Intersect Hydra voting](https://docs.hydra-voting.intersectmbo.org).&#x20;

**2. On-chain ratification** seats them. An _Update Constitutional Committee_ governance action goes on-chain carrying the elected credentials. It requires **67% DRep approval and 51% SPO approval** to ratify, and takes effect at the following epoch boundary.

The second half is where elections are actually won or lost. The off-chain vote is a recommendation; only the on-chain action appoints anyone.

***

### Who does what

Since January 2026, **Intersect's governance team executes** and the **Civics Committee oversees**. The arrangement was approved by seven votes in favour on [29 January 2026](../../meeting-minutes/2026-civics-meeting-minutes/civics-minutes-29-jan-26.md), conditional on a written process description and a RACI matrix.

Intersect provides the platform, verifies applications, coordinates the timeline and submits the governance action. Civics retains oversight, including adjudicating edge cases such as incomplete or non-genuine applications. Intersect does not control the outcome and cannot appoint members. Appointment happens only through on-chain ratification.

This replaced the volunteer working group model, so that running an election no longer depends on volunteer availability.

***

### Standing as a candidate

Candidacy is open. You dont need to be an Intersect member. Information about the next election cycle will be made public on the Intersect Knowledge Base.

***

### The record

| Election                     | Result                                                                                                                                                               | Source                                                                                                                                                                                            |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Interim CC** (2024)        | Process approved by unanimous vote with one recusal: open candidacy via Summon, two-stage, stake-weighted top three. Term set at 73 epochs from the Chang hard fork. | [Intersect Knowledge Base](https://docs.intersectmbo.org/intersect-knowledge-base/archive/cardano-governance-archive/governance-roles/constitutional-committee/interim-constitution-committee-cc) |
| **2025 election**            | Voting tool selected by competitive RFP. Governance action submitted July 2025, timed to the 580/581 epoch boundary.                                                 | [Intersect Knowledge Base](https://docs.intersectmbo.org/intersect-knowledge-base/cardano-facilitation-services/cardano-governance/2025-constitutional-committee-elections)                       |
| **Snap election** (Dec 2025) | 72 votes across 2.878bn ADA, approximately 21% of active voting power, exceeding the preceding full election.                                                        | [Intersect Knowledge Base](https://docs.intersectmbo.org/intersect-knowledge-base/cardano-facilitation-services/cardano-governance/2025-cc-snap-election-overview)                                |
| **2026 election**            | Ratified 1 September 2026, enacted 6 September 2026.                                                                                                                 | [Intersect Knowledge Base](https://docs.intersectmbo.org/intersect-knowledge-base/cardano-facilitation-services/cardano-governance/2026-constitutional-committee-elections)                       |

***

### 2026 in detail

**Hydra voting, 28 June – 23 July 2026**

|                     |                                 |
| ------------------- | ------------------------------- |
| Seats contested     | 4 of 7                          |
| Candidates          | 10 (after a two-week extension) |
| DReps voting        | 38                              |
| Participating power | 2.33bn ADA (epoch 645 snapshot) |
| Invalid ballots     | **0**                           |

**On-chain, 31 July – 1 September 2026**: governance action [`gov_action1w2w…fsggt5`](https://adastat.net/governances/729daaf2f9f89f842a61f6e3ebf7e57d16d6fa4116e29c13114780cb3909085000)

|              |                                |
| ------------ | ------------------------------ |
| Ballots cast | 522                            |
| DReps voting | 184 (5.08bn ADA active power)  |
| SPOs voting  | 338 (10.99bn ADA active power) |
| DRep support | **71.95%**: threshold 67%      |
| SPO support  | **56.54%**: threshold 51%      |

Registration originally closed on 4 June with exactly four candidates for four seats, a ballot offering no choice. The committee voted six in favour, none against, one abstention to extend by two weeks ([4 June 2026](../../meeting-minutes/2026-civics-meeting-minutes/civics-minutes-04-jun-26.md)), ran targeted outreach across Intersect, the Cardano Foundation, IOG and community channels, and the field reached ten.

The independent audit reconstructed the result from source records, verified file integrity by SHA-256 hash, validated the Hydra close and fanout transactions, reproduced the on-chain result hashes, and published the complete raw audit package.

Published results and timeline: [2026 Constitutional Committee Elections](https://docs.intersectmbo.org/intersect-knowledge-base/cardano-facilitation-services/cardano-governance/2026-constitutional-committee-elections).

***

### Next cycle

The next Constitutional Committee election is expected in 2027. Watch this page, the [Weekly Intersect Newsletter](https://intersectmbo.org/news), [@Intersectmbo](https://x.com/intersectmbo) and [@intersectCIVICS](https://x.com/intersectCIVICS) for updates.

If you are considering standing, the most useful thing you can do now is to familiarize yourself with these [resources](resources.md).

[**Why Intersect facilitates an election process to confirm a new Constitutional Committee**](https://www.intersectmbo.org/news/why-intersect-facilitates-an-election-process-to-confirm-a-new-constitutional-committee)
