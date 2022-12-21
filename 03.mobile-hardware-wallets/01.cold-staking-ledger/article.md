---
title: 'Setup Cold Staking With Ledger Hardware Wallet'
taxonomy:
    category:
        - 'Mobile Wallets'
    author:
        - 'The PIVX Team'
classifier:
    active: true
    tags:
        -
            tag: table
            nums: '\*'
            class: tutotable
---

! NOTE: The following guide is for Ledger Only; Don't use Trezor addresses for cold staking, as PET4L cannot spend P2CS utxos yet.

**Prerequisites:**
  * A Ledger wallet with the PIVX app installed​
  * The latest PIVX wallet from https://pivx.org​/downloads
  * Download and install PET4L (PIVX Emergency Tool For Ledger) from https://github.com/PIVX-Project/PET4L/releases​

![1.hw-wallet.png](1.hw-wallet.png?classes=center&resize=450)

Using image above as a reference, follow the following steps:
1. Unlock PIVX Wallet, choose "Unlock Wallet" from small drop down menu​
2. Wait until wallet is connected and fully synchronized with PIVX blockchain​
3. Press “Snowflake” icon to enable "Cold Staking" tab​
4. Press “Cold Staking” tab​
5. Press “Staker“​
6. Press “Create Cold Staking Address”​

![2.hw-wallet.png](2.hw-wallet.png?classes=center&resize=450)

Using image above as a reference, continue with the following steps:
7. Enter an easy to identify Label​
8. Press “Generate”​

![3.hw-wallet.png](3.hw-wallet.png?classes=center&resize=450)

Using image above as reference, Continue with the following:
9. Press “My Cold Staking Addresses“​
10. Press the new cold stake address​
11. Press “Copy” from small pop-up menu​

![4.hw-wallet.png](4.hw-wallet.png?classes=center&resize=450)

Almost done! Using the image above as a reference, finish with just a few more steps:
12. Press “Delegation“ tab​
13. Paste the address you copied in step 11​
14. Enter amount of PIV you wish to stake​
15. Enter an easy to identify label if you wish​
16. Paste an unused hardware wallet address (see below if you don’t know how)​
17. And finally, press “Delegate“​

**Recommended Final Steps**

Lock PIVX wallet (see step 1 above)
Unlock PIVX Wallet (see step 1 above) choosing for Staking Only
You are now Cold Staking with your PIV safely stored on your hardware wallet

**Additional Information**

1. To spend your rewards, you will need to use the PET4L program.

2. Your hardware wallet will probably NOT show Cold Staking balance, however, you can see it on the official PIVX block explorer
https://explorer.pivx.org/​
​
3. You can also create a desktop shortcut for faster access, just modify this url with your own address:
https://explorer.pivx.link/address/ReplaceWithColdStakingAddressFromStep16​
​
4. Adding more PIV to your cold stake, using image above as reference:
13. Drop down and select existing cold staking address​
14. Enter amount of PIV you want to add to your cold stake​
15. Skip this step, (will fill in automatically in step 14 above)​
16. Drop down and select the address with the label you used in step 7 above​
17. Press "Delegate"​

**Getting Hardware Wallet Address for Cold Staking**

Open PET4L program and unlock hardware wallet with PIVX app

![5.hw-wallet.png](5.hw-wallet.png?classes=center&resize=450)

Using image above as a reference, follow the steps below:
1. Verify PIVX Server is connected​
2. Connect to Hardware device​
3. Load / Refresh addresses from hardware wallet​
4. Dropdown addresses list and select an unused address​
5. Click “Copy“ icon to copy address​
6. Close PET4L​
7. Paste address in PIVX wallet (step 16 above)​
