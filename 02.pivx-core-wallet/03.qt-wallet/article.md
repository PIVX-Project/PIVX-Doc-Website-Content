---
title: 'PIVX QT Core Wallet'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

The **PIVX QT Wallet** is a GUI (graphic user interface) version of the PIVX core wallet and works on most desktop operating systems.  The following image is from the **Home** tab:

![1.Homepage.png](1.Homepage.png?classes=center,img-fluid)

The RED annotations in the image above refer to the following:  
1. **Main menu**
2. **Current balances:**
  * Available: Spendable PIVs
  * Pending: PIVs pending confirmation (requiring confirmations to be available for spending)
  * Immature: PIVs corresponding to staking transactions (requiring confirmations to be available for staking)
3. **List of all transactions on the wallet**. Hover over a transaction to see the confirmations count, click to access the details.
4. **List of all Staking Rewards** received, in a graph form.
5. **Synchronization status:** Grey means synchronization is in progress. White means that your wallet is fully synchronized. Hovering over the icon will provide more details on the sync status (such as latest block number and timestamp)
6. **Staking status:** turns white when staking is enabled
7. **Cold Staking status:** turns white when cold staking is enabled
8. **Active connection count:** clicking on it provides more details on network stats
9. **TOR status:** turns white when the wallet is connected via the TOR network
10. **Wallet locking status:** show if the wallet is locked/controls the locking status between the 4 possible states:
  * Wallet unencrypted: This is the initial state. It is recommended to encrypt your wallet as soon as you start using it.
  * Wallet Locked: No transactions can be input on the wallet.
  * Wallet unlocked: Wallet is unlocked for spending and for staking.
  * Staking only: Wallet is unlocked only for staking, no transactions can be input.
11. **Theme selection:** Switch between light and dark themes
12. Link to **Wallet FAQ**
13. **QR Code** that corresponds to your PIVX address. Clicking on it enlarges the QR code and displays your address.

### Tabs of the Core Wallet

[plugin:page-inject](/pivx-core-wallet/qt-wallet/qt-wallet-tabs)