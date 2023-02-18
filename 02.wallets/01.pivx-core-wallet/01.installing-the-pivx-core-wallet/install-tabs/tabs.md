---
title: 'Install Tabs'
taxonomy:
    author:
        - 'The PIVX Team'
tabitems:
    -
        name: linux
        title: Linux
        content: " 1. Navigate to the folder where you want to install the PIVX Core Wallet (for example **cd /home/pivx/pivx**)\n 2. Download the latest version of the Core Wallet: **wget https://github.com/PIVX-Project/PIVX/releases/download/v[version]/pivx-[version]-xxx** (link from pivx.org website) \n 3. Unzip the archive: **tar -zxvf pivx-[version]-aarch64-linux-gnu.tar.gz && sudo rm -f pivx-[version]-aarch64-linux-gnu.tar.gz** \n 4. Navigate to the newly created folder **cd pivx-[version]**\n 5. *First install only:* Install the Sapling parameters (Keys securing Shield transactions) by running the command **./install-params.sh** \n 6. Launch the PIVX server **./pivxd -daemon**, or the PIVX GUI client: **./pivx-qt** \n"
    -
        name: windows
        title: Windows
        content: " 1. Download the latest version of the Core Wallet from https://pivx.org/downloads \n 2. Run the installer and follow all steps.\n 3. Launch the PIVX Core Wallet.\n"
    -
        name: macos
        title: MacOS
        content: " 1. Download the latest version of the Core Wallet from https://pivx.org/downloads \n 2. Run the installer and Copy the PIVX App to Applications folder.\n 3. Launch the PIVX Core Wallet.\n"
---

