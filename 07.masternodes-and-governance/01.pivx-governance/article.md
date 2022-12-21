---
title: 'PIVX Governance'
taxonomy:
    category:
        - 'Masternodes And Governance'
    author:
        - 'The PIVX Team'
---

PIVX is a DAO (Decentralized Autonomous Organization); it has no employees, no management, only community members who got together to advance the project.

Although a significant portion of the work is done by volunteers, a monthly budget of 43'200 PIV is allocated to proposals submitted by the community and voted upon by masternode owners (1 masternode = 1 vote).

PIVX creates a new block every 60 seconds; each of these blocks create 5 new PIVs, with 1 PIV for any treasury proposals (3 PIV go to a masternode owner, 2 PIV go to the staker who wrote the block).

Rules of the road:
* Anyone can submit a proposal to the network (submission costs 50 PIV).
* It is a good practice to post a pre-proposal on the PIVX forum (to obtain feedback from the community) prior to submitting the proposal to the network.
* To be funded, a proposal has to receive a 'yes' vote from at least 10% of the masternodes.
* If the total amount of funded proposals is above 43'200, proposals with the most 'yes' votes are funded first.

All proposals are visible on the dedicated section of the PIVX website: [PIVX Proposals](https://pivx.org/proposals)

### Drafting a proposal

1. Discuss your proposal with the community on Discord to gauge interest from the community/refine your idea
2. Detail it in a forum post in the [pre-proposal section](https://forum.pivx.org/forums/pre-proposal-discussions.5/)
3. Gather feedback from the community. Adjust the content of the proposal and budget accordingly.
4. Create the final proposal in the [Budget & Governance Proposals Section](https://forum.pivx.org/forums/budget-governance-proposals.4/)

! NOTE: Please make sure you follow the guidelines/format documented on the sticky posts in the forum, to make it easy for masternode owners to decide on your proposal.

### Creating a proposal using the pivx-cli command line client or the debug console

Once the proposal is ready, you will need to submit it to the network so that masternode owners can vote on it. This is done via the core wallet that will be paying the 50 PIV fee.

! NOTE: Please review the status of the current budget cycle on [PIVX Proposals](https://pivx.org/proposals) prior to submitting the proposal. Make sure masternode owners will have enough time to vote on the proposal, and that there is enough budget in the next cycle to accommodate it.

Once you're ready to submit, run the following commands, either using the pivx-cli command line client or the debug console:
1. Obtain the next superblock (starting block) number:
	```
	getnextsuperblock
	```
2. Prepare the Proposal
	```
	preparebudget < name of proposal > < Forum link > < number of payments > < starting superblock > < payment address > < Amount per payment >
	```
3. Record the preparation hash
4. Submit the proposal to the network
	```
	submitbudget < name of proposal > < Forum link > < number of payments > < starting superblock > < payment address > < amount per payment > < preparation hash >
	```
5. Record the voting hash; add it to the forum post along with voting options, using the below template:
	```
	Proposal Name: < Proposal Name >
	hash= < voting hash >
	To vote yes:
	“mnbudgetvote many < vote hash > yes”
	To vote no:
	“mnbudgetvote many < vote hash > no”
	To check the status
	"getbudgetinfo < name of proposal >”
	```
	
! NOTE: Post from new forum members (New Pivians) require validation from an Admin before they are visible to others. If that happens to you, post a message on Discord to let the admins know they have a post to validate.