---
title: 'Core Wallet Best Practices / FAQ'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

# General Questions
[faqs]
[faq question="My balance is 0 or is incorrect.  Where are my PIVs?"]
Make sure your wallet is fully synchronized. If your wallet is partially synchronized it will only show a partial balance.
[/faq]
[faq question="I had zPIVs and they don't appear in my wallet anymore. How do I recover them?"]
zPIVs have been retired several years ago following the change of protocol from Zerocoin to Shield. The grace period that was provided for recovery is now over so any zPIV not transfered before that date cannot be recovered.
[/faq]
[faq question="How do I backup my Wallet?"]
### Backup Using PIVX Core QT Wallet
![1.backup_wallet.png](1.backup_wallet.png?classes=center,img-fluid)

From the PIVX Core QT wallet as above:
1. Select "SETTINGS"
2. Select "Wallet Data"
3. Select "Wallet"
4. Open "Select folder ..." and browse for a location on you computer to store the backup.
5. Save your PIVX wallet.dat into the directory of your choosing.  You can name it whatever you like but when restoring a wallet, it must always be named wallet.dat.

#### Backup Using A File Manager
1. Shutdown your PIVX Core Wallet
2. Navigate to the the PIVX data folder. Default locations are as follows:
  * Windows: %appdata%/pivx 
  * Linux: ~/.pivx 
  * MacOS: ~/Library/Application Support/PIVX
3. Locate the wallet.dat file and copy it to a safe place
[/faq]
[/faqs]

### Core Wallet
[faqs]
[faq question="I can't get my PIVX Core Wallet to start. When I try to run it nothing happens, an error is displayed, the window disappears, the loading window never completes, or another startup issue is encountered."]
This may be caused by an abnormal shutdown of the wallet resulting in corruption of your local blockchain data.  

1. Make a backup of your wallet.dat.
2. Try using the `-forcestart` startup flag to see if it will recover from a failed start.
  * If using Windows GUI, you will need to make a shortcut to the pivx-qt.exe file with the `-forcestart` flag.
  * You can run pivxd daemon with the switch `-forcestart` from the command line of all operating systems. 

If the above does not resolve the startup issue, try to resync the blockchain.
[/faq]
[/faqs]

### Blockchain Syncronisation
[faqs]
[faq question="My wallet has stopped syncing at block xxx. How can I fix it?"]
The first step is to confirm whether you are on the right chain. To do so, follow these steps:  
* Run the `getbestblockhash` command in the debug console
* Check whether that block is available from a PIVX block explorer like https://zkbitcoin.com 
* If it is not available there, your core wallet is on a forked chain and needs to be resynced from scratch (see below for steps)

If you're using the QT wallet, the steps are all summarized on the picture below:  

![2.fork_check.png](2.fork_check.png?classes=center,img=fluid)  

[/faq]
[faq question="How did my Core Wallet end up being on a forked chain?"]
There are a few possibilities, among which:  

* Connecting to 'bad' peers that veer you onto an orphan chain.
* Having too few peers, making net consensus less reliable.
* General connectivity issues (network speed, reliability).
[/faq]
[faq question="How do I resync my core wallet from scratch?"]
1. Stop the wallet.
2. Make a backup of your wallet.dat file.
3. Start the wallet.
4. Go to Settings --> Debug --> Wallet Repair --> Delete local blockchain.
5. Wait for resync to complete.

From the command line, stop the wallet then run the command `pivxd -daemon -resync`
[/faq]
[faq question="Does PIVX provide official blockchain snapshots? How do I create my own blockchain snapshot?"]
No, there is no official blockchain snapshot.

You 
can however create your own if you don't want to have to download the full blockchain in case you need to reinstall the core wallet. Here are the steps:  

1. Shut down your wallet (not doing so will result in a corrupted snapshot)
2. Navigate to the the PIVX data folder. Default locations are as follows:
  * Windows: %appdata%/pivx 
  * Linux: ~/.pivx 
  * MacOS: ~/Library/Application Support/PIVX
3. Take a backup of the following folders:
  * Blocks
  * Chainstate
  * Sporks
  * Zerocoin
4. Zip these folders and keep them safe.

Should you ever need to restore your blockchain snapshot, follow this procedure:  
1. Shutdown your wallet.
2. Delete these folders:
  * Blocks
  * Chainstate
  * Sporks
  * Zerocoin
3. Extract the snapshot zip file into the data folder
4. Start wallet, the syncing will resume from the last block stored in the snapshot.
[/faq]
[/faqs]

