---
title: 'Staking with PIVX Core Wallet'
taxonomy:
    category:
        - Staking
    author:
        - 'The PIVX Team'
---

Staking with the PIVX Core Wallet requires very little setup.

### Step-by-step setup

1. Launch PIVX Core Wallet & make sure it is synchronized
![Synchronized Wallet](1.synchronized_wallet.png?classes=center&resize=600)

2. Make sure the PIV you have in your wallet have at least 600 confirmations; this can be checked by hovering/clicking on any transaction in the core wallet
![Confirmed Transaction.png](2.confirmed_transaction.png?classes=center&resize=300)

3. Unlock your core wallet for staking
  * In the PIVX Command line Wallet, type **pivx-cli walletpassphrase YourWalletPassPhrase 9999999 true**
  * In the PIVX QT Wallet, click on Wallet Locked/Staking Only, enter your password and confirm
![Unlock For Staking](3.unlock_for_staking.png?classes=center&resize=300)

4. Confirm that staking is active by checking the status of the icon on top of the core wallet
![Staking Active](4.staking_active.png?classes=center&resize=300)

Staking status can also be checked using the following command line: **./pivx-cli getstakingstatus**

5. Enjoy your staking rewards, that will appear as transactions in your core wallet
![Staking Transaction](5.staking_transaction.png?classes=center&resize=300)

### Troubleshooting staking issues
For any issues related to staking activation / rewards, please make sure you read the relevant FAQ at [Troubleshooting Staking](/staking/staking-faq)

If your problem is not documented in the FAQ, feel free to raise it on the PIVX Discord.
