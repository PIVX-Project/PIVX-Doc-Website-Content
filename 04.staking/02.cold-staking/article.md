---
title: 'Cold-Staking your PIV'
taxonomy:
    category:
        - Staking
    author:
        - 'The PIVX Team'
---

Cold Staking consists in delegating the staking of your PIVs to an online ('Hot') wallet while they remain safely stored in an offline ('Cold') wallet.

The cold wallet can be:
* An instance of PIVX Core Wallet, that is brought up online only to stake/spend your PIVs.
* A hardware wallet (such as the ones provided by Ledger or Trezor)

The hot wallet can be:
* A dedicated PIVX Core Wallet node that you run yourself, in order to leave your coins safely offline
* A PIVX Staking service ran by a specialized service provider such as (http://www.allnodes.com)
* A Core Wallet ran by a member of the PIVX community, as a courtesy to other community members

### Step-by-step setup (Command-line client)

These steps are shared between the Owner Wallet ("Cold Wallet") and the Staker Wallet ("Hot Wallet"). If you control both wallets, you'll have to run all of them sequentially. If someone is providing you with a staking service each party will have to run his own steps sequentially.

1. Staker Wallet: Generate a “staking address” using that command line:
	```
	pivx-cli getnewstakingaddress
	```
! NOTE: You don’t need to create a new staking address for each delegation. You can reuse your previously generated addresses. To list them, use the command:

	```
	pivx-cli liststakingaddresses
	```
	
2. Owner Wallet: Generate an “owner address” (if you don’t have one already):
	```
	pivx-cli getnewaddress
	```
	
3. Owner Wallet: Create a “cold stake delegation” in favor of the Staking Address:
	```
	pivx-cli delegatestake "Staker Address" Amount "Owner Address"
	```
	
	! NOTE: If the owner address is omitted, a new address is automatically generated from the wallet.
	
	! NOTE: If you want to delegate to an external address (using an owner address not present in the wallet, e.g. one from a hardware device), then you need to add true at the end of the command (check pivx-cli help delegatestake for more info).
	
	
	
4. Staker Wallet: Whitelist the owner address on your staker wallet (if you haven’t already).
	```
	pivx-cli delegatoradd <ownerAddress>
	```

	! NOTE: Once a delegator address is whitelisted, it remains so, including for successive delegations. To remove a particular address from the whitelist, run:
	```
	pivx-cli delegatorremove <ownerAddress>
	```

	! NOTE: To view the current whitelisted addresses, do
	```
	pivx-cli listdelegators
	```

To send additional delegations, using the same addresses-pair, re-run step 3 of this guide.

! NOTE: The 'hot' wallet has to be 'Unlocked for staking'

### Step-by-step setup (QT client)

These steps are shared between the Owner Wallet ("Cold Wallet") and the Staker Wallet ("Hot Wallet"). If you control both wallets, you'll have to run all of them sequentially. If someone is providing you with a staking service each party will have to run his own steps sequentially.

1. Staker Wallet: Generate a “staking address”
  * Navigate to the "Cold Staking" section / "Staker" tab of the core wallet
  * Click on the "Create Cold Staking Address" menu (Input your wallet passphrase if locked)
  * Input the required details (address Label is for your reference only)
  * Click 'Generate' and share the address/QR Code with the owner of the Owner Wallet (see step 3)
! NOTE: You don’t need to create a new staking address for each delegation. You can reuse your previously generated addresses. To list them, click on "My Cold Staking Addresses" on the main cold staking screen

![Manage Staking Addresses.png](1.manage_staking_addresses.png?classes=center&resize=450)

2. Owner Wallet: Generate an “owner address” (if you don’t have one already):
	```
	pivx-cli getnewaddress
	```
	
3. Owner Wallet: Create a "cold stake delegation” in favor of the Staking Address:
  * Navigate to the "Cold Staking" section / "Delegation" tab of the core wallet
  * Input the cold staking address/label generated at step 1 (or communicated by your cold staking provider)
  * Input the amount to delegate
  * Input the owner address generated at step 2 (If the owner address is omitted, a new address is automatically generated from the wallet)
  * You can use the 'Coin Control' menu to select the exact UTXO you want to cold stake

![Manage Staking Addresses.png](1.manage_staking_addresses.png?classes=center&resize=450)
	
4. Staker Wallet: Whitelist the owner address on your staker wallet (if you haven’t already). This is done from the command line/debug console:
	```
	pivx-cli delegatoradd <ownerAddress>
	```

	! NOTE: Once a delegator address is whitelisted, it remains so, including for successive delegations. To remove a particular address from the whitelist, run:
	```
	pivx-cli delegatorremove <ownerAddress>
	```

	! NOTE: To view the current whitelisted addresses, do
	```
	pivx-cli listdelegators
	```

To send additional delegations, using the same addresses-pair, re-run step 3 of this guide.

! NOTE: The 'hot' wallet has to be 'Unlocked for staking'

### Troubleshooting staking issues
For any issues related to staking activation / rewards, please make sure you read the relevant FAQ at [Troubleshooting Staking](/staking/staking-faq)

If your problem is not documented in the FAQ, feel free to raise it on the PIVX Discord.