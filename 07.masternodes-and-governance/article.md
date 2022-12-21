---
title: 'Masternodes And Governance'
taxonomy:
    category:
        - 'Masternodes And Governance'
    author:
        - 'The PIVX Team'
---

Discover the PIVX Governance model and get started with your Masternode

===

PIVX has a two-tier network of nodes, with the first tier including common wallets and staking nodes and the second comprised of masternodes. Masternodes support voting on PIVX budget proposals as well as experimenting with the future addition of special features, such as instant transactions. They also strengthen the overall network through incentivized software updates and online availability.

Unlike for PIVX stakers, who receive rewards at random, masternode income is more predictable. PIVX produces a new standard block on average every minute. (There is also a superblock made roughly once per month that pays for budget items that have been voted on by the masternodes.) Each block makes a single masternode payment. The masternode paid by any given block is selected from a deterministic list of all masternodes, and the paid masternode is moved to the back of the list after the payment. Each payment is 3 PIV.

You can estimate your annual returns over a period of time by dividing that time in minutes by the estimated number of masternodes to get the number of payments and then multiplying that by 3 to get the number of PIV. For example, for around 1600 masternodes over 30 days, your masternode will earn approximately (minutes/masternodes)x3 = (30x24x60/1600)x3 = 81 PIV.

## Requirements for Running a PIVX Masternode

To run a masternode, you will need 10,000 PIV. Exactly 10,000 PIV must be sent in a single transaction output (called a UTXO) to an address you control. The private key for this address will be used to sign the one-time transaction that starts the masternode after the masternode software is running (more on that below). 

Running a masternode requires running masternode software, which is an online PIVX wallet specially configured to be a masternode. It must be continuously running, without a break of more than two hours, or it will be penalized through a delay in its ability to get a next payment. 

This masternode software can either be outsourced, using a service like Allnodes or nodehub.io, or self-hosted. Outsourcing the masternode software is a popular choice for many, as it removes the technical burden of running and maintaining the online masternode software and can be acquired for only $5-10/month.

Self-hosting requires more technical knowledge and responsibility, but gives greater control. And it helps PIVX because it is beneficial to the network to have as many independent entities as possible managing masternode software. Hosting a masternode requires a single-processor computer with a recommended minimum of 2 GB RAM, 50 GB disk space, and 2 TB of monthly data.

A good source for this computer is a Virtual Private Server (VPS) purchased from providers like Vultr, Digital Ocean, or others. After acquiring a VPS, you will need to download and install the latest PIVX wallet, set the configuration file pivx.conf for masternode operation, and run pivxd, the PIVX daemon. This software, the first time it is run, will take several hours to sync the blockchain, and after that have minimal maintenance.

With the masternode software running and up to date on the blockchain, you will then create a transaction that starts the masternode. Software exists to help with this, including the PIVX Core wallet and the Secure PIVX Masternode Tool (SPMT). SPMT provides a graphical interface for handling multiple nodes with easy access to payout balances, enablement checking, and estimates to the next payout.

## How Do I Start

You first need to decide if you want to self-host your masternode software or outsource it. If you want to outsource it, you can go to the provider, such as [Allnodes](https://www.allnodes.com), and follow their directions to start the software and start the masternode. 

If you are self-hosting, you will need to acquire a VPS and download and run the software. You can follow general instructions for using the PIVX Core wallet for masternodes given in [General Masternodes](/masternodes-and-governance/masternodes) or detailed instructions on setting up a Digital Ocean VPS and configuring it using the SPMT software with Ledger Wallet given in [Running a Masternode on Digital Ocean](/masternodes-and-governance/hosting-on-digital-ocean).

## Troubleshooting Masternode Issues

If you have issues with your masternode, they may have already been solved by others. Please check the relevant FAQ at [Troubleshooting Masternodes](/masternodes-and-governance/masternodes-faq).

If your problem is not documented in the FAQ, feel free to raise it on the PIVX Discord.




