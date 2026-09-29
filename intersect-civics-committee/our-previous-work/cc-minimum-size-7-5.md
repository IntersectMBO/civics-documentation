# CC minimum size 7 → 5

The Constitutional Committee has a minimum size set on-chain by a protocol parameter, `committeeMinSize`. If the committee ever drops below it, it cannot act, and the constitutional review of governance actions stops until the committee is refilled.

Until July 2026 that floor was seven, the same as the number of seats. With seven members required and seven filled, a single resignation would have taken the committee below its minimum and frozen its work, for the months it takes to elect and seat a replacement on-chain.

The Civics committee recommended lowering the floor to five, so that losing one or two members can no longer halt governance, while keeping the _intended_ committee size at seven or more. Five is a resilience floor, not a target.

### What Civics did

The change began as a recommendation from the Parameter Committee and the Technical Steering Committee. Civics evaluated it and reached consensus to support it on 19 March 2026, with the understanding that the desired working size of the committee should remain seven or more.

Civics then drafted a formal recommendation to the TSC to submit the parameter change as soon as possible (9 April 2026). Submission was gated on the Plutus cost model update moving through the network first, which pushed the timing back through May (7 May, 14 May 2026).

The on-chain action needed 75% approval to pass, and Civics tracked and promoted it through the voting window to enactment.

### Outcome

The parameter change was **enacted on-chain on 13 July 2026**, reducing `committeeMinSize` from 7 to 5.

The committee's position throughout was that five is a floor for resilience. The intended working size of the Constitutional Committee remains seven or more.

[**On-chain governance action**](https://adastat.net/governances/c75bb221606687aa858ec89c7a15c88e9c17054f2e045ae31ecc8a9687cd206e00)

[**Understanding the committeeMinSize Governance Action**](https://x.com/IntersectCIVICS/status/2062964547720249604?s=20)
