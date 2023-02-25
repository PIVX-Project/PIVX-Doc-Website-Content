---
title: 'Cold Staking Your PIVX'
taxonomy:
    category:
        - Staking
    author:
        - 'The PIVX Team'
---

**Cold Staking** is the process of delegating the staking of your PIVX to a _Hot Wallet_ while your PIVX remain safely stored offline in a _Cold Wallet_.

The _Cold Wallet_ can be:
* A PIVX Core Wallet running seperately from the _Hot Wallet_.
* [MyPIVXWallet](/wallets/my-pivx-wallet "MyPIVXWallet")
* A hardware wallet such as a Ledger.  Note that Trezor is currently NOT supported.

The _Hot Wallet_ can be:
* A PIVX Core Wallet running seperately from the _Cold Wallet_.
* A PIVX Cold Staking service by a staking service provider such as:
  * [MyPIVXWallet](/wallets/my-pivx-wallet "MyPIVXWallet")
  * [PIVX Toolbox](https://toolbox.pivx.org/cold-staking "PIVX Toolbox")
  * [AllNodes](http://www.allnodes.com "AllNodes")
* A PIVX Core Wallet operated by a member of the PIVX community as a courtesy to other community members.

### Step By Step Guide - QT Client

These steps are shared between the _Cold Wallet_ (Owner) and the _Hot Wallet_ (Staker). If you control both wallets, you'll have to run all of these steps seperately. If someone is providing you with a staking service, each party will have to run the respective steps.

1. _Hot Wallet_ (Staker): Generate a “staking address”
  * Navigate to the "Cold Staking" -> "Staker" tab of the core wallet.
  * Click on the "Create Cold Staking Address" menu (input your wallet passphrase if locked).
  * Input the required details (address label is for your reference only).
  * Click "Generate" and share the address with the owner of the _Cold Wallet_.  

!!! **NOTE** - You don’t need to create a new staking address for each delegation. You can reuse your previously generated address. To list them, click on "My Cold Staking Addresses" on the main cold staking screen.

![Manage Staking Addresses.png](1.manage_staking_addresses.png?classes=center,img-fluid,py-4)

2. _Cold Wallet_ (Owner): Generate an “owner address” (if you don’t have one already):
	```
	pivx-cli getnewaddress
	```
	
3. _Cold Wallet_ (Owner): Create a "cold stake delegation” in favor of the Staking Address:
  * Navigate to the "Cold Staking" section / "Delegation" tab of the core wallet
  * Input the cold staking address/label generated at step 1 (or communicated by your cold staking provider)
  * Input the amount of PIV to delegate
  * Input the owner address generated at step 2 (If the owner address is omitted, a new address is automatically generated from the wallet)
  * You can use the 'Coin Control' menu to select the exact UTXO you want to cold stake

![Manage Staking Addresses.png](1.manage_staking_addresses.png?classes=center,img-fluid,py-4)
	
4. _Hot Wallet_ (Staker): Whitelist the owners address (if you haven’t already done so). You can do this from the command line debug console:
	```
	./pivx-cli delegatoradd <ownerAddress>
	```

	!!! **NOTE** - Once a delegator's address is whitelisted, it remains so, including for successive delegations. To remove a particular address from the whitelist, run the command: `./pivx-cli delegatorremove <ownerAddress>`.   You can view the current whitelisted addresses by running the command `./pivx-cli listdelegators`

To send additional delegations, using the same addresses-pair and re-run step 3 of this guide.

!!! **NOTE** - The _Hot Wallet_ must be "Unlocked for Staking"


### Step By Step Guide - Command Line Client

These steps are shared between the _Cold Wallet_ (Owner) and the _Hot Wallet_ (Staker). If you control both wallets, you'll have to run all of these steps seperately. If someone is providing you with a staking service, each party will have to run the respective steps.

1. _Hot Wallet_ (Staker): Generate a “staking address” using the command: `./pivx-cli getnewstakingaddress`  

!!! **NOTE** - You don’t need to create a new staking address for each delegation. You can reuse a previously generated address. To list them, use the command `./pivx-cli liststakingaddresses`
	
2. _Cold Wallet_ (Owner): Generate an “owner address” (if you don’t have one already): `./pivx-cli getnewaddress`
	
3. _Cold Wallet_ (Owner): Create a “cold stake delegation” in favor of the Staking Address: `./pivx-cli delegatestake "Staker Address" Amount "Owner Address"`
	
	!!! **NOTE** - If the owner address is omitted, a new address is automatically generated from the wallet. If you want to delegate staking to an external address (using an owner address not present in the wallet, for example, one from a hardware device), then you need to add `true` at the end of the command (check `./pivx-cli help delegatestake` for more info).  
	
4. _Hot Wallet_ (Staker): Whitelist the owner address on your wallet (if you haven’t done so already): `./pivx-cli delegatoradd <ownerAddress>`

	!!! **NOTE** - Once a delegator address is whitelisted, it remains so, including for successive delegations. To remove a particular address from the whitelist, run the command: `./pivx-cli delegatorremove <ownerAddress>`.  To view the current whitelisted addresses, run the command `./pivx-cli listdelegators`  

To send additional delegations, using the same addresses-pair, re-run step 3 of this guide.

!!! **NOTE** - The _Hot Wallet_ must be "Unlocked for Staking"

### Troubleshooting Staking Issues

For any issues related to staking activation / rewards, please make sure you read the relevant FAQ at [Troubleshooting Staking](/staking/faq)  