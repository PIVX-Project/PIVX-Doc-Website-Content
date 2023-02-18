---
title: 'PIVX QT Core Wallet'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
media_order: '1.Homepage.png,cold-staking.png,contacts.png,masternodes.png,receive.png,send.png,settings.png'
---

The **PIVX QT Wallet** is a GUI (graphic user interface) version of the PIVX core wallet and works on most desktop operating systems.  The following image is from the **Home** tab:

![qt-home.png](qt-home.png?classes=center,img-fluid)

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

### Core Wallet Tabs Menu

[tabs]
[tab title="SEND"]
![send.png](send.png?classes=center,img-fluid)  

This tab is used to send PIVs to another wallet, to transfer PIVs between multiple addresses in your wallet and to shield or unshield PIVs. The procedure to send PIVs:  

1. Select the coins you want to **spend** (Transparent or shielded). The available balance at the bottom will reflect the total PIVs for that coin type.  
2. Enter the recipient address (it can be transparent or shielded); you can also pick one from your contacts. Adding a label will add the address to your contacts.
3. Enter the amount you want to send. Depending on who needs to pay the fee, using the 'Substract fee from amount' checkbox:
  * If 'Substract fee from amount' is checked, your wallet will be debited the exact amount you input. The recipient will receive **Amount - fee**
  * If 'Substract fee from amount' is unchecked, your recipient will receive the exact amount you input. Your wallet will be debited **Amount + fee**
 4. If you're sending to a shielded address, you can add an encrypted memo for the recipient (not available for transparent addresses)
 5. If you want to spend specific UTXOs, you can use the 'Coin Control' dialog to select the PIVs you want to send. It can be useful if you are staking and want to keep particular UTXOs untouched so they don't have to wait 600 confirmations before they can stake again. You can also customize the address on which the 'change' (unspent amount on the UTXOs you selected) has to be sent.
 6. All the transaction characteristics will be summarized in a single dialog when you click Send. If you're ok with the details click on 'SEND'. The transaction will be broadcast to the network instantly for confirmation.  
  
Steps 2 to 4 can be made simpler if your counterparty generated a 'payment request' URL. In that case you can paste it in the 'Open URI' dialog to have the address, label, and amount auto-populated:  

[plugin:youtube](https://www.youtube.com/embed/M2BYEZe4u7E)

!!! **NOTE** - Shielding/Un-shielding coins is as simple as sending them to one of your Shield/Transparent address.  

[/tab]
[tab title="RECEIVE"]
![receive.png](receive.png?classes=center,img-fluid)  

The Receive tab is used to manage your own addresses. You can flip between Transparent and Shield addresses using the toggle button on top.  

When a new wallet is created you will have a default address and can then create as many addresses as you need (potentially a new address for each payment/counterparty to enhance privacy), by clicking the 'Generate Address' button.  

All your addresses can be listed by clicking on 'My Addresses'.  

Each address from the list (selected by clicking on it) will then have:  

1. The address itself
2. A QR code (that can be flashed with mobile wallets to avoid retyping the address)
3. A label (for your own use only)  

[/tab]
[tab title="CONTACTS"]
![contacts.png](contacts.png?classes=center,img-fluid)  

This is your contacts list. You can input all the third-party addresses you use regularly (e.g. regular payment addresses, exchanges, etc.) for easier access:  

[plugin:youtube](https://www.youtube.com/embed/U7O_C2bKuDk)  

[/tab]
[tab title="MASTERNODES"]
![masternodes.png](masternodes.png?classes=center,ing-fluid)  
Visit the [Masternodes](/masternodes) section for more details.  

[/tab]
[tab title="COLD STAKING"]
![cold-staking.png](cold-staking.png?classes=center,img-fluid)  
Visit the [Cold Staking](/staking/cold-staking) section for more details.  

[/tab]
[tab title="SETTINGS"]
![settings.png](settings.png?classes=center,img-fluid)  
This tab contains both Qt Wallet GUI configuration options (in the Options tab) and Advanced Configuration / Wallet debugging options, detailed in the [PIVX Core Wallet Advanced Features](/wallets/pivx-core-wallet/wallet-debugging-features) section  

[/tab]
[/tabs]

