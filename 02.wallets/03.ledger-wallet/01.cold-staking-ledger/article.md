---
title: 'Setup Cold Staking With A Ledger Hardware Wallet'
---

!!! **NOTE** - The following guide is for Ledger hardware wallets ONLY. Do NOT use Trezor addresses for cold staking as PET4L software cannot currently spend P2CS utxos.

**Prerequisites:**
  * A Ledger wallet with the PIVX app installed​
  * The latest PIVX wallet from https://pivx.org​/downloads
  * Download and install PET4L (PIVX Emergency Tool For Ledger) from https://github.com/PIVX-Project/PET4L/releases​

![1.hw-wallet.png](1.hw-wallet.png?classes=img-fluid,py-4)

Using the image above as a reference, follow these steps:
1. Unlock the PIVX core wallet, choose "Unlock Wallet" from small drop down menu​
2. Wait until the wallet is connected and fully synchronized with PIVX blockchain​
3. Press “Snowflake” icon to enable the "Cold Staking" tab​
4. Press “Cold Staking” tab​
5. Press “Staker“​
6. Press “Create Cold Staking Address”​

![2.hw-wallet.png](2.hw-wallet.png?classes=center,img-fluid,py-4)

Using the image above as a reference, continue with the following steps:
7. Enter an easy to identify Label​
8. Press “Generate”​

![3.hw-wallet.png](3.hw-wallet.png?classes=center,img-fluid,py-4)

Using the image above as a reference, continue with the following steps:
9. Press “My Cold Staking Addresses“​
10. Press the new cold stake address​
11. Press “Copy” from small pop-up menu​

![4.hw-wallet.png](4.hw-wallet.png?classes=center,img-fluid,py-4)

**Almost done!** Using the image above as a reference, finish with just a few more steps:
12. Press “Delegation“ tab​
13. Paste the address you copied in step 11​
14. Enter amount of PIV you wish to stake​
15. Enter an easy to identify label if you wish​
16. Paste an unused hardware wallet address (see below if you don’t know how)​
17. And finally, press “Delegate“​

### **Recommended Final Steps**

Lock your PIVX wallet then unlock choosing for Staking Only (see step 1 above). You are now Cold Staking with your PIV safely stored on your hardware wallet.

### **Additional Information**

* To spend your rewards, you will need to use the [PET4L](https://github.com/PIVX-Project/PET4L) software.
* Your hardware wallet may not show your Cold Staking balance, however, you can see it on a block explorer like [https://zkbitcoin.com](https://zkbitcoin.com)​
* You can create a desktop shortcut for faster access, just modify this URL with your address: `https://zkbitcoin.com/address/Replace-With-Address-From-Step-16`​
​
* Adding more PIV to your cold stake (see image above for reference):
  13. Drop down and select existing cold staking address​
  14. Enter amount of PIV you want to add to your cold stake​
  15. Skip this step, (will fill in automatically in step 14 above)​
  16. Drop down and select the address with the label you used in step 7 above​
  17. Press "Delegate"​

### **Getting A Hardware Wallet Address for Cold Staking**

Open the PET4L program and unlock your hardware wallet then select the PIVX app

![5.hw-wallet.png](5.hw-wallet.png?classes=center,img-fluid,py-4)

Using the image above as a reference, follow these steps:
1. Verify that the PIVX Server is connected​
2. Connect to the Hardware device​
3. Load / Refresh addresses from the hardware wallet​
4. Dropdown addresses list and select an unused address​
5. Click “Copy“ icon to copy the address​
6. Close PET4L​
7. Paste the address in PIVX wallet (see step 16 above)​
