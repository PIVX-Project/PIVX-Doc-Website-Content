---
title: 'PIVX Core Wallet Debugging Features'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

The PIVX Core Wallet contains a wealth of advanced troubleshooting/debugging features, that can be used to diagnose any issues and finetune your configuration.

### Wallet Data

That section contains options to backup your data:
1. Backup the wallet.dat file
2. Set or update a passphrase for your wallet
3. Export accounting (export all transactions as a csv file)
4. Export address book (to create a backup of the addresses in your address book)

### Tools

1. Sign/Verify message can be used to authenticate a message and prove that it's been written by the owner of a given address and transmitted unaltered
2. BIP38 Tool can be used to store/transmit your Key pair safely. All you have to remember is the passphrase you set at the time of encryption (it doesn't need to be the same as your core wallet passphrase).

### Options

That section contains display options for the GUI wallet

### Debug

The Debug tab is divided into 3 subtabs:
* **Information:** this is where you go to display all information pertaining to your wallet (equivalent command-line option **pivx-cli getinfo**)
  1. General info such as version, location of data folder
  2. Network information (Number of connections and masternodes)
  3. Blockchain information (latest block/sync timestamp, latest block hash)
* **Console:** This is the debug console. In that screen, you can execute all the commands that can be passed via the Command Line wallet.
* **Wallet Repair:** contains a set of functions that allows you to correct a corrupted/forked wallet.

!! WARNING: The Debug console is a very sensitive tool, that can be used to extract information from the wallet/process transactions. To avoid being scammed, make sure you always understand the commands you type there, especially if they have been sent to you by someone offering support.

!! WARNING: You can access the documentation/examples for any console functions by typing **help command**. For example **help dumpprivkey** to access the doc on the **dumpprivkey** function.
