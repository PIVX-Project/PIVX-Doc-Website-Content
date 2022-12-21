---
title: 'Installing the PIVX Core Wallet'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

### System Requirements

To run the PIVX Core Wallet, you need a system with the following specificqtions:
* Operating System: Windows, Linux, or MacOS
* CPU: At least 2GHz
* RAM: 2GB (4GB recommended)
* Disk Space: At least 25GB available

### Downloads

The latest version of the Core wallet can be found on (https://pivx.org/downloads).

!! NOTE Always download the Core wallet from the official website/Github

### Installation

[plugin:page-inject](/pivx-core-wallet/installing-the-pivx-core-wallet/install-tabs)

### Startup / initial synchronisation

The first time you run the Core Wallet, the whole PIVX blockchain will be downloaded locally and verified. This will take approximately 5 hours with a faast internet connection, and will require approximately 20GB of space on disk.

An empty wallet will also be created (stored in a **wallet.dat** file in the PIVX data folder).

### Upgrades

The PIVX Core Wallet is upgraded on a regular basis, in order to deliver new functionalities and fix bugs. There are two main types of releases:
* Mandatory releases: The mandatory releases generally either add functionalities to the wallet or to the network (e.g. cold staking) and/or fix critical issues. They have to be installed by all users before a given date (enforcement date), that is communicated by the developers at the time the release is published.
* Recommended/Optional releases: Optional releases are recommended for everyone but can generally be skipped safely. They either apply to only a subset of users (e.g. fix impacting masternodes only), or fix non-critical issues.

!! NOTE All releases are communicated on the pivx.org website and on the #important-updates channel of the PIVX Discord server. It is critical to review them and install all updates before the enforcement block, in order to avoid technical issues that could result in lost PIVs.

The procedure to upgrade the wallet is similar to an installation and is as easy as:
* Shutdown current version of the wallet.
* Install the new version of the core wallet by following the procedure corresponding to your system.
* Restart the core wallet using the newly installed version.



