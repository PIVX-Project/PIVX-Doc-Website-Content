---
title: 'Creating a Proposal'
---

Once the proposal is ready, you will need to submit it to the network so that masternode owners can vote on it. This is done via the core wallet that will be paying the 50 PIV submission fee.

!!! **NOTE** - Please review the status of the current budget cycle on [PIVX Proposals](https://pivx.org/proposals) prior to submitting the proposal. Make sure masternode owners will have enough time to vote on the proposal, and that there is enough budget in the next cycle to accommodate it.

### Using the pivx-cli Command Line Client or the Debug Console

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
5. Record the voting hash and add it to the forum post along with voting options, using the following template:
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