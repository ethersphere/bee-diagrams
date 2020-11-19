# Swarm roundtable
###### tags: `meeting notes`, `roundtable`

## Meta
When: weekly on Thursday, 1415 CET
Room: meet.jit.si/SwarmDev
Goal: brainstorm and discussions on everything Swarm
Agenda: Everybody can put a topic on the agenda. To do so, just create an item for the day that you want to speak. Subsequently, mention this in the #teamHQ channel in the Beehive.
## Notes

### 19.11
- Swarm API technical discussion, some questions (Attila):
    - What should go the lower-level layers and upper-level layers?
    - plans for removing APIs?
    - questions about current API
    - https://github.com/ethersphere/bee/issues/937
    - https://github.com/ethersphere/bee/search?q=api&type=issues
- Implications of latest PSS changes (Vojtech):
    - Can not calculate overlay address used for PSS from ETH public key anymore (our demo for the next Swarm event relies on this)
    - Question: Do we want to support a flow where users can contact any ETH address? (assuming it runs Bee)

### 11.11
- Scarce gBZZ (see document in #teamhq)

### 5.11.
- Remember, remember, the 5th of November (Gregor)
- How to be a collective knowledge creator in Roam (Gregor and Gašper presentation on conventions using Roam)
    - https://roamresearch.com/#/app/swarm-org/page/wgX6x6K84
- Javascript team roadmap plans, gathering feedback (Attila)


### 28.10
- Presentation on Zenhub workflows for the team: https://hackmd.io/j5kV_JjBRI6gdG8ZTVi2yw?both
- research update: push sync synching strategy, incentivization and blackhole problem
- short discussion what ports to use for bee, 8080 is quite popular port and it would be better to move away from it
    - we can define ports triplet for api, p2p and debug-api, maybe some 4 digit number has some meaning for swarm team

### 22.10
- SWAP with chequebook (see [swap with chequebook](https://hackmd.io/3GO4_kHXSD2rq6AX95ubzw)).
- Call to action: make your Github org membership public and maybe win a [](https://etherscan.io/token/0x73cdea750fa77fd87acdfb20ee2f9f0cda744333)

### 15.10
- Deprecate old Swarm codebase and cluster

### 8.10
- Infra testing on larger scale (Vandot)

### 1.10
- Bee packaging (Vandot)
    - what to support (OSes, distribution, archs...)
        - agreed to support Linux and MacOS
        - agreed to support deb and rpm with systemd
        - agreed to support brew for MacOS
            - @vandot to check support for system service integration
        - goreleaser has support for scoop (windows package manager)
            - @vandot to check options for scoop
    - how to solve dependency installations (clef and geth)
        - agreed for clef and geth, and any further dependency, point inside docs to official docs for those deps and how-tos
        - agreed that we will set and maintain our own geth node that would be a default endpoint for package installation
            - @juR-WWIFRuOFECyBhCoHog  to check what endpoints/calls with need to protect to maintain user privacy
            - @vandot to check how to provide that protection

### 17.09

### 10.09

- clef rules

### 6.08
- Bee code cleanup and improvements (janos)

### 30.07
- Pupa app (https://github.com/ethersphere/bee/issues/432)
- Ethereum signature support (see message @tmm360 in #core)

### 23.07
- nothing so far
### 16.07
- Accounting protocol discussion (Ralph, https://hackmd.io/t7AlcAaZRlyjX-A0GmnfJA)

Problem: how do we know what is the payment threshold. 
Solution: 
    - peers communicate the payment threshold in a handshake + update message in a separate protocol 
    - Any communicated payment threshold should be regarded by the other node as the threshold from which he might be disconnected
    - Hence, other nodes will send a payment at (or just before) this threshold.
    - The disconnect threshold is set by the node some reasonable margin (to account for natural fluctuation in balances) about the communicated payment threshold.
    - It is possible to update this threshold and trigger the protocol to send an update message, but we don't expose an API to do this (for now). Also, we don't expose the possibility to set the threshold which your node communicates in the beginning.
    - Ralph will make an issue to document this

- Persisting balances on disk (Rinke)
Problem: writing balances to disk continuously is a lot of IO-overhead. Rinke argued that it is ok to just forget the balances of your peers when you disconnect and let peers also to forget the balances of peers that disconnected from them. An exploit to this is possible, by disconnecting and re-connecting, but Rinke suspects it's just not worth the effort and if it ever becomes the effort to do so, we can easily patch it.
The majority of the call seemed to disagree with this and the proposed solution that is easiest is to write the balances to a batch and periodically write the batch to disk. This would prevent io contention and also makes an exploit not possible. 
We also spoke about the possibility of nodes "surfing" the network, by continuously making new identities or just not making any costs anymore just before the threshold. A solution to this is to communicate a very low initial payment threshold and gradually increase this.

### 09.07
[- Interface BOS <> code](https://hackmd.io/7jeS9qPqSeeAnmgQYMnlMg) (Rinke)
- Multiple open chunk retrieval line timing strategy (Abel)

### 02.07
- packaging and distribution of bee (vandot)
- incentives architecture (ralph) (https://hackmd.io/@ethswarm/H1qvBIjC8#/)

### 04.06
- global pinning publisher discussion (Viktor, Vojtěch, Santi, Marce)

### 28.05
- Global Pinning progress in Swarm
  - presentation: https://hackmd.io/mrc3z5Y-S4-lQ2N0faNGoA?view
  - dev questions
     - push sync/mode "put re-upload" 
     - `bzzkeyhex`/`bzzaccount`/`enode` meaning/impact
     - `oaddr` from boot-up log VS `oaddr` from `admin_peers`
     - publisher → public key process

notes: give an overview, take questions and ask questions

Elad: It seems as if we have a need to encode more information in the hash. Can we somehow encode more information in the hash? => https://multiformats.io/multihash/


### 21.05
- Proposal for manifests; structure and implementation (elad, louis). See:
https://holbrook.no/tmp/manifests/


 