# FairFlow Details

### How EG is calculated

**Off-chain**

* Whenever the aggregator algorithm produces a route for a user’s request that **includes FF pools**, a fair price calculation is triggered through collaboration between the aggregator and the FF backend.
* The **additional value** contributed by the FF pools is determined as the **difference** between: ◦ The best route **including FF pools**, and&#x20;
  * The best alternative route **excluding FF pools**.
* A portion of this additional value is recognized as **potential EG**.&#x20;
  * The **remaining value** stays embedded in the route to ensure the taker still gets a competitive rate.
* Based on the calculated potential EG, the FF backend computes a **fair price** and generates a **signature** for it.
  * This signed fair price is then included in the user’s transaction.

**On-chain**

* When the transaction reaches the blockchain, the **hook** checks the signed fair price against the **actual on-chain output** of the FF pools.
* **If the actual result from the FF pools is better than or equal to the signed fair price**:
  * The pools deliver the **fair price result** to the taker.&#x20;
  * The pools absorb the difference internally (the EG).&#x20;
* **If the actual result is worse than the fair price**:&#x20;
  * The pools instead deliver the **actual on-chain result** to the taker.
  * No EG is absorbed in this case.

### How EG sharing is distributed

EG sharing for each position will be calculated and be displayed in near real-time, with approximately a 5-minute delay after blockchain confirmation. These rewards will accumulate over a fixed cycle, currently set to 7 days. At the end of each cycle, a new cycle will begin immediately.

The rewards from the completed cycle will enter a validation period of up to 48 hours. Once validated, our internal system will transfer the accumulated EG sharing funds to the distribution smart contract.

The accumulated EG sharing will be split between the LP Pool and Kyber (as the hook owner), with 70% allocated to the LP Pool and 30% to Kyber (This ratio is subject to change based on prevailing policies or governance decisions).
