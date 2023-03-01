---
title: 'Installing the PIVX Core Wallet'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

### System Requirements

To run the PIVX Core Wallet, you need a system with the following specifications:
* **Operating System**: Windows, Linux, or MacOS
* **CPU**: At least 2GHz
* **RAM**: 2GB (4GB recommended)
* **Disk Space**: At least 25GB available

### Downloads

The latest version of the Core wallet can be downloaded from the official [PIVX website's download](https://pivx.org/downloads) page **or** from the official [PIVX github](https://github.com/PIVX-Project/PIVX/releases/latest) page.

!! **WARNING** - Always download the PIVX Core Wallet from one of these official resources.  Any downloads from any other source should be considered compromized.

### Installation
The installation method differs based on the operating system being used.

[tabs]
[tab title="Linux"]
1. Navigate to the folder where you want to install the PIVX Core Wallet (for example `cd /home/pivx`)  
2. Download the latest version of the Core Wallet:  
  * Intel/AMD: `wget https://github.com/PIVX-Project/PIVX/releases/download/v[version]/pivx-[version]-x86_64-linux-gnu.tar.gz`  
  * ARM: `wget https://github.com/PIVX-Project/PIVX/releases/download/v[version]/pivx-[version]-arm-linux-gnueabihf.tar.gz`  
3. Unzip the archive:
  * Intel.AMD: `tar -zxvf pivx-[version]-aarch64-linux-gnu.tar.gz && sudo rm -f pivx-[version]-x86_64-linux-gnu.tar.gz`  
  * ARM:  `tar -zxvf pivx-[version]-arm-linux-gnueabihf.tar.gz && sudo rm -f pivx-[version]-arm-linux-gnueabihf.tar.gz`  
4. Navigate to the newly created folder `cd pivx-[version]`  
5. **First install only:** Install the Sapling parameters by running the command `./install-params.sh`  

6. Navigate to the **_bin_** folder: `cd bin` then start the wallet:
  * CLI Wallet: `./pivxd -daemon` 
  * QT Wallet: `./pivx-qt`   


[/tab]
[tab title="Windows"]
1. Download the latest version of the Core Wallet from https://pivx.org/downloads.
2. Run the installer and follow all steps.
3. Launch the PIVX Core Wallet.

[/tab]
[tab title="MacOS"]
1. Download the latest version of the Core Wallet from https://pivx.org/downloads.
2. Run the installer and Copy the PIVX App to Applications folder.
3. Launch the PIVX Core Wallet.

[/tab]
[/tabs]

### Startup / Initial Synchronisation

The first time you run the PIVX Core Wallet, the whole PIVX blockchain will be downloaded locally and verified. This will take approximately 5+/- hours with a fast internet connection, and will require approximately 20GB of space on disk.

An empty wallet will also be created (stored in a **wallet.dat** file in the PIVX data folder).

### Upgrades

The PIVX Core Wallet is upgraded on a regular basis, in order to deliver new functionalities and fix bugs. There are two main types of releases:
* **Mandatory Releases**: The mandatory releases generally either add functionalities to the wallet or to the network (e.g. cold staking) and/or fix critical issues. They have to be installed by all users before a given date known as the _enforcement date_ which is communicated by the developers at the time the release is published.
* **Recommended/Optional Releases**: Optional releases are recommended for everyone but can generally be skipped safely. They either apply to only a subset of users (e.g. fix impacting masternodes only) or to fix non-critical issues.

!!! **NOTE** - All releases are communicated on the official [PIVX Website](https://pivx.org) and on the **#important-updates** channel of the [PIVX Discord](https://discord.pivx.org) server. It is critical to review them and install all updates before the enforcement block in order to avoid technical issues.

The procedure to upgrade the wallet is similar to an installation and is as easy as:
* Shutdown the current version of the wallet.
* Install the new version by following the procedure corresponding to your operating system.
* Restart the core wallet using the newly installed version.