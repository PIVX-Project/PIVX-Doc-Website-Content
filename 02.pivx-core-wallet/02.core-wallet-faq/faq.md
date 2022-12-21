---
title: 'Core Wallet Best Practices / FAQ'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
faqitems:
    -
        generic: null
        sectiontitle: 'Generic Questions'
        questions:
            -
                question: 'My balance is 0 or is incorrect; where are my PIVs?'
                response: 'Make sure your wallet is fully synchronized; if your wallet is partially synchronized it will only show a partial balance.'
                shortcut: incorrect_balance
            -
                question: 'I bought PIVs a few years ago and haven''t opened my wallet for ages. I had zPIVs and they don''t appear in my wallet anymore. How do I recover them?'
                response: 'zPIVs have been retired several years ago following the change of protocol (from Zerocoin to Shield). The grace period that was provided for recovery is now over so any zPIV not transfered before that date cannot be recovered.'
                shortcut: zpiv
            -
                question: 'How do I backup my Wallet data?'
                response: "![1.backup_wallet.png](1.backup_wallet.png?classes=center&resize=600)\n #### In the QT/GUI PIVX as above:\n 1. Open the PIVX wallet, Select \"settings\"\n 2. Select \"Wallet Data\"\n 3. Select \"Wallet\"\n 4. Select the box which states \"Select folder ...\"\n 5. Save your PIVX wallet.dat in the directory of your choosing and name it whatever you like; when loading it into your PIVX wallet directory it must always be named wallet.dat.\n\n\n#### Via file browser:\n 1. Shutdown your PIVX Core Wallet\n 2. Navigate to the the PIVX data folder; default values are:\n * On Windows: %appdata%/pivx\n * On Linux: ~/.pivx\n * On MacOS: ~/Library/Application Support/PIVX\n 3. Locate the wallet.dat file and copy it to a safe place\n"
                shortcut: backup
    -
        corewallet: null
        sectiontitle: 'Core Wallet'
        questions:
            -
                question: 'I Can''t get my Core Wallet to start. When I try to run it nothing happens, an error is displayed, the window disappears, the loading window never completes, or another startup issue is encountered.'
                response: "This can be caused by an abnormal exit of the wallet, resulting in corruption of your local blockchain cache.\n 1. Make a backup of your wallet.dat\n 2. Try using the -forcestart startup flag to see if it will recover from a failed start (If using Windows GUI, you will need to make a shortcut to the pivx-qt.exe file with the -forcestart flag; From the command line on all operating systems you can call the pivxd daemon with the switch -forcestart)\n If the above does not resolve the startup issue, try to resync the blockchain."
    -
        issues: null
        sectiontitle: 'Blockchain Synchronisation'
        questions:
            -
                question: 'My wallet has stopped syncing at block xxx. How can I fix it?'
                response: "The first step is to confirm whether you are on the right chain. To do so, follow the following steps:\n * Run the **getbestblockhash** command in the debug console\n * Check whether that block is available on the PIVX explorer: https://explorer.pivx.link/\n * If it is not available there, your core wallet is on a forked chain, and needs to be resynced from scratch (see below for steps)\n If you're using the QT wallet, the steps are all summarized on the picture below:\n ![2.fork_check.png](2.fork_check.png?classes=center&resize=600)"
                shortcut: forked_chain
            -
                question: 'How did my Core Wallet end up being on a forked chain?'
                response: "There are a few possibilities, among which:\n * Connecting to 'bad' peers that veer you onto an orphan chain.\n * Having too few peers, making net consensus less reliable.\n * General connectivity issues (net speed, reliability)."
                shortcut: forked_chain_why
            -
                question: 'How do I resync my core wallet from scratch?'
                response: " 1. Stop the wallet.\n 2. Make a backup of your wallet.dat file.\n 3. Start the wallet.\n 4. Go to Settings --> Debug --> Wallet Repair --> Delete local blockchain.\n 5. Wait for resync to complete.\n\nSteps 3/4 can also be ran from the command line using: **pivxd -daemon -resync**"
                shortcut: resync
            -
                question: 'Does PIVX provide official blockchain snapshots? How do I create my own blockchain snapshot?'
                response: "No, there is no official blockchain snapshot.\n You can however create your own if you don't want to have to download the full blockchain in case you need to reinstall the core wallet. Here are the steps:\n 1. Shut down your wallet (not doing so will result in a corrupted snapshot)\n 2. Navigate to your PIVX data directory. Default values are:\n - %appdata%/pivx on Windows\n - ~/.pivx on Linux\n - ~/Library/Application Support/PIVX on MacOS\n 2. Take a backup of the following folders:\n - Blocks\n - Chainstate\n - Sporks\n - Zerocoin\n 3. Zip these folders and keep them safe. Should you ever need to restore your blockchain simply copying over these folders to the same data directory mentioned above will allow your PIVX wallet to resume from where this snapshot was taken in terms of block height synced."
                shortcut: snapshot
---

