---
title: 'Staking with PIVX Core Wallet'
taxonomy:
    category:
        - Staking
    author:
        - 'The PIVX Team'
---

Staking with the PIVX Core Wallet requires very little setup.

### Step By Step Guide

1. Launch the PIVX Core Wallet and make sure it is fully synchronized.  
![Synchronized Wallet](1.synchronized_wallet.png?classes=center,img-fluid,py-4)

2. Make sure the PIV you have in your wallet have at least 600 confirmations. This can be checked by hovering/clicking on any transaction in the core wallet.  
![Confirmed Transaction.png](2.confirmed_transaction.png?classes=center,img-fluid,py-4)  

3. Unlock your core wallet for staking only:
  * PIVX QT Wallet - click on Wallet Locked/Staking Only, enter your password and confirm  
  * PIVX CLI Wallet - type `./pivx-cli walletpassphrase YourWalletPassPhrase 9999999 true`  
![Unlock For Staking](3.unlock_for_staking.png?classes=center,img-fluid,py-4)  

4. Confirm that staking is active:
  * PIVX QT Wallet - check the status from the icon on the top of the core wallet
  * PIVX CLI Wallet - type `./pivx-cli getstakingstatus`


![Staking Active](4.staking_active.png?classes=center,img-fluid,py-4)

5. Enjoy your staking rewards.  Rewards will appear as transactions in your wallet  

![Staking Transaction](5.staking_transaction.png?classes=center,img-fluid,py-4)

### Troubleshooting Staking Issues
For any issues related to staking activation or rewards, please make sure you read the [FAQ - Troubleshooting Staking](/staking/faq) page.  

If your issue is not documented in the FAQ, feel free to reach out on the [PIVX Discord](https://discord.pivx.org).