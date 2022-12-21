---
title: 'QT Wallet Tabs'
taxonomy:
    author:
        - 'The PIVX Team'
tabitems:
    -
        name: SEND
        title: SEND
        content: "![2.SEND.png](2.SEND.png?classes=center&resize=600)\n\n This tab is used to send PIVs to another wallet, to transfer PIVs between multiple addresses in your wallet and to shield or unshield PIVs.\n The procedure to send PIVs:\n 1. Select the coins you want to **spend** (Transparent or shielded). The available balance at the bottom will reflect the total PIVs for that coin type.\n 2. Enter the recipient address (it can be transparent or shielded); you can also pick one from your contacts. Adding a label will add the address to your contacts.\n 3. Enter the amount you want to send. Depending on who needs to pay the fee, using the 'Substract fee from amount' checkbox:\n * If 'Substract fee from amount' is checked, your wallet will be debited the exact amount you input. The recipient will receive **Amount - fee**\n * If 'Substract fee from amount' is unchecked, your recipient will receive the exact amount you input. Your wallet will be debited **Amount + fee**\n 4. If you're sending to a shielded address, you can add an encrypted memo for the recipient (not available for transparent addresses)\n 5. If you want to spend specific UTXOs, you can use the 'Coin Control' dialog to select the PIVs you want to send. It can be useful if you are staking and want to keep particular UTXOs untouched so they don't have to wait 600 confirmations before they can stake again. You can also customize the address on which the 'change' (unspent amount on the UTXOs you selected) has to be sent.\n 6. All the transaction characteristics will be summarized in a single dialog when you click Send. If you're ok with the details click on 'SEND'. The transaction will be broadcast to the network instantly for confirmation.\n\n\nSteps 2 to 4 can be made simpler if your counterparty generated a 'payment request' URL. In that case you can paste it in the 'Open URI' dialog to have the address, label, and amount auto-populated:\n <center><iframe width='470' height='291' src='https://www.youtube.com/embed/M2BYEZe4u7E' title='YouTube video player' frameborder='0' allow='accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture' allowfullscreen></iframe></center>\n\n!!! NOTE: Shielding/Un-shielding coins is as simple as sending them to one of your Shield/Transparent address."
    -
        name: RECEIVE
        title: RECEIVE
        content: "![3.RECEIVE.png](3.RECEIVE.png?classes=center&resize=600)\n\n The Receive tab is used to manage your own addresses. You can flip between Transparent and Shield addresses using the toggle button on top. \n When a new wallet is created you will have a default address and can then create as many addresses as you need (potentially a new address for each payment/counterparty to enhance privacy), by clicking the 'Generate Address' button. \n  All your addresses can be listed by clicking on 'My Addresses'.\n\n Each address from the list (selected by clicking on it) will then have:\n 1. The address itself \n 2. A QR code (that can be flashed with mobile wallets to avoid retyping the address)\n 3. A label (for your own use only)\n"
    -
        name: CONTACTS
        title: CONTACTS
        content: "![4.CONTACTS.png](4.CONTACTS.png?classes=center&resize=600)\n\n This is your contacts list. You can input all the third-party addresses you use regularly (e.g. regular payment addresses, exchanges, etc.) for easier access: \n <center><iframe width='470' height='291' src='https://www.youtube.com/embed/U7O_C2bKuDk' title='YouTube video player' frameborder='0' allow='accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture' allowfullscreen></iframe></center>"
    -
        name: MASTERNODES
        title: MASTERNODES
        content: "![5.MASTERNODES.png](5.MASTERNODES.png?classes=center&resize=600)\n\n Head-out to the [Masternodes And Governance](/masternodes-and-governance) section for more details.\n"
    -
        name: COLDSTAKING
        title: 'COLD STAKING'
        content: "![5.5COLDSTAKING.png](5.5COLDSTAKING.png?classes=center&resize=600)\n\n Head-out to the [Cold Staking](/staking/cold-staking) section for more details.\n"
    -
        name: SETTINGS
        title: SETTINGS
        content: "![6.SETTINGS.png](6.SETTINGS.png?classes=center&resize=600)\n\n That tab contains both Qt Wallet GUI Configuration options (in the Options tab) and Advanced Configuration / Wallet debugging options, detailed in the [PIVX Core Wallet Advanced Features](/pivx-core-wallet/wallet-debugging-features) section "
---

