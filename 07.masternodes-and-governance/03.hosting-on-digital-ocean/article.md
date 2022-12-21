---
title: 'Hosting a PIVX Masternode On Digital Ocean '
taxonomy:
    category:
        - 'Masternodes And Governance'
    author:
        - 'The PIVX Team'
---

# Hosting a PIVX Masternode On Digital Ocean 
# *With PIV Held Using a Ledger*

##Background

A PIVX masternode is configured wallet software running online backed by 10,000 PIV that lets you to vote on budget proposals and earn rewards. Running one is a great way to both support PIVX and add to your holdings.

Setting up a masternode not as hard as it might sound. This article will describe how to do it using a Virtual Private Server (VPS) hosted on Digital Ocean ([https://www.digitalocean.com](https://www.digitalocean.com)). Digital Ocean is regarded by the PIVX community as being good for masternodes, with high uptime.

Running a masternode requires holding 10,000 PIV in an account you control. Signing the transaction that starts the masternode is the only place in the process where the private key for these funds interacts with the network. To minimize risk in this step, this article uses a Ledger hardware wallet for storing the private key. 

## Masternode Requirements

The masternode software is just the standard PIVX Core wallet software specially configured. It needs to download the PIVX blockchain, and once downloaded, it needs to keep information on the blockchain in memory to operate efficiently. It also has to get and send update information continually with peers.

This operation leads to the following recommended system requirements:

1. 1 Intel CPU 
2. 50 GB SSD storage
3. 2 GB RAM
4. 2 TB data transfer per month
5. Ubuntu 20.04

## Configuring the Masternode VPS

A VPS instance meeting the above requirements can be acquired at Digital Ocean at the time of this writing for $10-12/month (the $12/month premium Intel processor was used when testing for this article). Through the Digital Ocean dashboard, you can create this VPS and start to use it right away.

When configuring the VPS, it is best to add a firewall. The masternode software uses port 51472, and the firewall can be set through the Digital Ocean dashboard to only allow UDP and TCP packets for this port.

From inside the Digital Ocean dashboard, you can invoke a command line console for your new VPS. This console opens inside a browser and gives all the functionality needed to run a masternode. There is no need to use SSH or other remote-interface software.

## Installing and Configuring the Masternode Software

**Step 1.** The first step after opening the Digital Ocean console for your new VPS is to install security patches. This can be done with the following command at the Linux prompt inside the console window:

`sudo apt-get update && sudo apt-get -y upgrade`

**Step 2.** Next, you should add 1 GB of swap space to the system. This may be needed during the initial sync of the PIVX blockchain. To add 1 GB swap space to your VPS, follow the instructions here: [https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-20-04).

**Step 3.** Get the latest PIVX wallet software (5.3.2 at the time of this writing) using the following command:

`cd ~ && wget https://github.com/PIVX-Project/PIVX/releases/download/v5.3.2/pivx-5.3.2-x86_64-linux-gnu.tar.gz`

If the latest release is something other than 5.3.2, replace “5.3.2” with the latest version number in the two places it is mentioned in the above line and similar places in the following steps—if past naming trends hold, this will work.

**Step 4.** Untar and unzip the file you just downloaded to install the wallet software:

`tar -zxvf pivx-5.3.2-x86_64-linux-gnu.tar.gz`

**Step 5.** Generate a Masternode private key using the Secure PIVX Masternode Tool (SPMT) software. First, download the SPMT software from [https://github.com/PIVX-Project/PIVX-SPMT](https://github.com/PIVX-Project/PIVX-SPMT), install, and run it. Then in the main window, click the “New Masternode” button to begin configuring a new masternode. It will bring up the following GUI:


![masternode-Tutorial1](51.SPMT.png?classes=center&resize=800)

In this GUI window, click the “Generate” button next to the "MN Priv Key" box. This will create a long string in the box that resembles the following:

![masternode-Tutorial2](52.SPMT.png?classes=center&resize=800)

That string is the masternode private key. Though the “private key” name suggests a need for extreme care, this string is not especially sensitive. It keeps others from using your masternode software to earn masternode rewards on their own 10,000 PIV, but your 10,000 PIV are not at risk from others learning it. This masternode private key will be used in the next step, and we will return to the SPMT GUI window later, in the next section (so keep it open for now). 

**Step 6.** Configure the wallet software to run as a masternode. Do this by first creating and editing&#151;using vi, in this example&#151;the configuration file with the following command:

`mkdir ~/.pivx && cd ~/.pivx && vi pivx.conf`

Then enter the following using the vi text editor (or an alternative of your choice) into the configuration file:

`   rpcuser=<username>`  
`   rpcpassword=<password>`  
`   rpcallowip=127.0.0.1`  
`   server=1`  
`   daemon=1`  
`   logtimestamps=1`  
`   maxconnections=256`  
`   masternode=1`  
`   externalip=<vpsip>`   
`   masternodeaddr=<vpsip>:51472`   
`   masternodeprivkey=<privkey>`   

There are five entries in the above, marked with <> angle braces. These you will need to enter as unique to your configuration. The entries for <username\> and <password\> can be anything you like, but the password should be hard to guess. You could use “user” and something like “QaCkD1Ju5Tu2iq1On3,” for example. This password limits general outside interaction with the masternode software. The two values for <vpsip\> can be the IPv4 address (in the form xxx.xxx.xxx.xxx) read off of the Digital Ocean dashboard. The value for <privkey\> should be the string captured from the SPMT software in Step 5 above.

**Step 7.** Install the sapling parameters that are used by PIVX’s cryptographic algorithms using the following command:

`cd ~/pivx-5.3.2/ && ./install-params.sh`

**Step 8.** Start the wallet software using the following:

`cd ~/pivx-5.3.2/bin && ./pivxd`

**Step 9.** Monitor and verify the running masternode software by watching the tail end of the debug.log file. This log file holds a variety of debug and progress status messages that are generated while the software runs. (Do not be alarmed by recurring notices of networking warnings, which are common and generally recoverable.) Here is the command to watch the ongoing new activity of the log file:

`tail -f ~/.pivx/debug.log`

Wait either for the message “Sync has finished” or for the message that the block number at the top of the PIVX blockchain has been accepted. You can learn this block from the official PIVX explorer at [https://explorer.pivx.link](https://explorer.pivx.link), where it is labeled “Last Indexed Block”. When this check passes, your masternode software is running and current!

## Posting 10,000 PIVX to Start the Masternode

You need 10,000 or more PIV. (If you don’t have this, you will need to buy it before continuing.) This example uses Ledger Live to control the funds, so, under that assumption, start by transferring exactly 10,000 PIV to a receive address for your Ledger. 

You can configure this receive address in Ledger Live by selecting “Add Account” in the Accounts page of Ledger Live to make a new PIVX account. After the account is created, you can learn its primary address by selecting to receive funds in that account and following prompts until the address is available. Send exactly 10,000 PIV to this address in a single transaction. Any other amount will not work to fund a masternode.

After you have exactly 10,000 from a single transaction available on Ledger Live, take the following steps (referring to the SPMT configuration-interface image from Step 5 of the last section):

**Step 1.** Name your node. The configuration window in the SPMT software should still be open from Step 5 of the last section (if it isn’t still open, it is easy to return to it by re-running SPMT, clicking on the “New Masternode” button to configure a new masternode, and re-entering the masternode private key that was generated in the last section). In the “Name” box, enter any name meaningful to you. “PIVX01” could be used, for example.

**Step 2.** Enter the masternode IP address into the "IP Address" box. This should be the same value used in the pivx.conf file created in Step 6 of the last section.

**Step 3.** Get the account number from Ledger Live. Every Ledger PIVX account has a number. This number is usually one less than the order they appear in the Ledger Live interface, so the first account is 0, the second account is 1, and so forth. Set the "Account" value to this number.

**Step 4.** Enter the PIVX address holding your 10,000 PIV into the "PIVX Address" box. This is the same as the receiving address used to hold the 10,000 PIV in Ledger Live. 

**Step 5.** Capture the address's public key into the "Public Key" box through the following procedure: With the account number and PIVX address already entered, and with your Ledger connected to your computer, click the “>>” button to capture the public key from the Ledger. A PIVX address is made by hashing the account's public key in a process that is not reversible. So it is necessary to go back to the Ledger to get this information.

**Step 6.** Capture the ID for the transaction that sent your 10,000 PIV into the "txid" box by clicking the "Lookup" button to get it. Additionally, in the usual case where the 10,000 PIV were sent in a simple transaction (one destination address for the 10,000 PIV and zero or one change address), the "txidn" (next to the "txid" box) will be 0.

**Step 7.** Click “Save” to save the information. Then click the rocket button next to the newly created masternode entry in the main GUI window to launch it. This will require using your Ledger to sign the transaction with the private key controlling the 10,000 PIV.

**Step 8.** Optionally, confirm the launch on the VPS masternode wallet by entering the following at the Linux prompt inside the console window for the VPS:

`cd ~/pivx-5.3.2/bin && ./pivx-cli getmasternodestatus`

You should get error-free information that includes the address holding 10,000 PIV and an affirming message.

With this launch, you are now an operator of a PIVX masternode! In a few minutes your new masternode will show as “ENABLED” in the SPMT software when you click the "Get Status of All Masternodes" button. And after a few days you will start earning regular rewards that will be deposited to the address holding your 10,000 PIV (but as different transaction outputs). Thank you for supporting the PIVX network and the privacy and liberty it offers.

##To Explore Further

Here are additional good online resources related to setting up and configuring PIVX masternodes. They contributed to this article and add additional information.

1. Allnodes hosts masternodes for those not wanting to run them themselves. Their instructions are also a good reference when setting up your own masternode. [https://help.allnodes.com/en/articles/3217223-how-to-setup-a-pivx-masternode-on-allnodes](https://help.allnodes.com/en/articles/3217223-how-to-setup-a-pivx-masternode-on-allnodes)

2. Bertrand Marlier gives insight  into setting up a masternode in his June 26, 2017 article. [https://medium.com/@bm842/setup-a-pivx-masternode-on-linux-3310fe6c36a2](https://medium.com/@bm842/setup-a-pivx-masternode-on-linux-3310fe6c36a2)

3. PIVX administrator Jeffrey describes how to host a masternode using Linux in this July 18, 2020 article. [https://forum.pivx.org/threads/how-to-host-a-pivx-masternode-if-you-are-using-linux-cli.707](https://forum.pivx.org/threads/how-to-host-a-pivx-masternode-if-you-are-using-linux-cli.707)

4. Jeffrey also wrote this PIVX masternode setup guide on September 3, 2020. [https://forum.pivx.org/threads/masternode-setup-guide.746](https://forum.pivx.org/threads/masternode-setup-guide.746)

5. Jude Zhu wrote this guide to setting up a masternode using Vultr on April 1, 2017. [https://judezhublog.wordpress.com/2017/04/01/how-to-set-up-pivx-master-node](https://judezhublog.wordpress.com/2017/04/01/how-to-set-up-pivx-master-node)

6. Le Petit Bloc wrote a descriptive article on the pivxd program in 2018. [https://hub.docker.com/r/lepetitbloc/pivxd](https://hub.docker.com/r/lepetitbloc/pivxd) 

7. A PIVX masternode explorer is available to find information on your and other masternodes. [https://explorer.masternodes.online/currencies/PIVX](https://explorer.masternodes.online/currencies/PIVX)















