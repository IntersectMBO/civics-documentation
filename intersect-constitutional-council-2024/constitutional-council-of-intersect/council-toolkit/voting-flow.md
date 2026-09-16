---
icon: box-ballot
---

# Voting Flow

Here we describe the end-to-end voting flow using the council toolkit for vote transaction signing.

### Proposed Steps

1. Deliberation and decision
   * Council meets and works asynchronously &#x20;
   * Council deliberate on action
   * Metadata drafting
   * Vote consensus reached by the council
   * Metadata finalization
2. Building vote transaction
   * Orchestrator coordinates with council to turn metadata into correct format.
   * Orchestrator construct an unsigned transaction incorporating the specific governance action and the council's chosen consensus on the governance action; Constitutional, Unconstitutional, or Abstain.
   * Orchestrator sends the unsigned vote transaction to each voter key-holder.
3. Signing the transaction via council toolkit
   * Each voter key signer uploads the transaction
   * Each voter inspects the transaction, ensuring it is correct
   * Each voter produces a signature for the vote transaction
4. Collecting the Signatures/Witnesses and submission
   * Orchestrator collects all signatures and assemble the finalised signed transaction.
   * Orchestrator does final checks and then submits the vote to chain.



