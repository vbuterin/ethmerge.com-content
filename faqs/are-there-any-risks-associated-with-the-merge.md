---
title: Are there any risks currently associated with "The Merge"?
weight: 9.0
attribution:
  -
    name: Lamboshi
    link: https://twitter.com/L_Nakaghini
  -
    name: "@InsideTheSim"
    link: https://twitter.com/InsideTheSim
  -
    name: "@VitalikButerin"
    link: https://twitter.com/VitalikButerin
---

There are two categories main risks associated with the merge:

* Risks in the **implementation**, eg. consensus failures
* Risks in the **mechanism**, eg. centralization and attacks once proof of stake is in place

There are always risks in implementation when making a large change to a protocol that is securing [hundreds of billions of dollars of assets](https://etherscan.io/stat/supply). These risks are being mitigated in several ways. First, the beacon chain itself will have had more than one year of operational time by the time the merge happens, and so far it has been running without issues. Second, there are multiple implementations of the Ethereum protocol, and the Ethereum core dev community has been strongly advocating for more client diversity, aiming for an outcome where no single client has more than 50% (ideally, more than 33%) of the network. In such a world, a bug in one single client will not greatly harm the network, as the other clients will keep running.

Risks in the mechanism have been mitigated through extensive research and analysis before and after the beacon-chain launch. Post-launch, ongoing research has already identified weaknesses in the spec (eg. [30% attacks](https://econcs.pku.edu.cn/wine2020/wine2020/Workshop/GTiB20_paper_8.pdf)), and there are well-understood fixes for them that are planned to be added before the merge.

The mechanism risk that is hardest to model is **centralization risk**. In simplest terms, a centralization risk arises when a validator with 10x the capital can earn more than 10x the rewards (or earn 10x the rewards with less than 10x the costs). Such situations are problematic both because they create dynamics where the rich get richer faster than the poor, and because they create incentives for individual stakers to join large staking pools instead of staking on their own.

Proof of work itself has plenty of centralization risks which proof of stake is immune to. However, proof of stake does have centralization risks of its own. The Ethereum spec development process has identified and heavily mitigated many centralization risks; there are two major remaining ones:

* **32 ETH staking minimum**: users with less than 32 ETH cannot directly stake, so can only join pools.
* **[MEV extraction](https://ethereum.org/en/developers/docs/mev/)**: there exist complicated strategies to optimize transaction fee revenue, and large pools are more well-suited to implement these strategies (note: this applies to both status-quo PoW Ethereum _and_ post-merge PoS Ethereum)

There are two paths being explored to solve the first issue. First, we can reduce the staking minimum in-protocol, and re-design the protocol so that this does not lead to node centralization from nodes needing to process attestations from an extremely large number of validators. **[Single slot confirmation](https://ethresear.ch/t/a-model-for-cumulative-committee-based-finality/10259)** is one approach being considered for this. Second, we can work on decentralized stake pooling software, so that users can form pools without having to trust central parties. **[Secret shared validators](https://medium.com/coinmonks/eth2-secret-shared-validators-85824df8cbc0)** are expected to accomplish this goal.

The main currently explored path to mitigating centralization risks from MEV extraction is **proposer/builder separation (PBS)**; see ethresear.ch [post 1](https://ethresear.ch/t/proposer-block-builder-separation-friendly-fee-market-designs/9725) and [post 2](https://ethresear.ch/t/two-slot-proposer-builder-separation/10980) and [slides](https://hackmd.io/@vbuterin/mev_presentation). PBS allows a separate class of actors ("builders") to optimize for MEV extraction while block proposers can accept their bundles through a simple auction mechanism, removing the need for block proposers (ie. validators) to optimize for MEV extraction themselves.
