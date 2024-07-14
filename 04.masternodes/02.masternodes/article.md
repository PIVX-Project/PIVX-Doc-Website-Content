---
title: 'General Masternodes'
taxonomy:
    category:
        - 'Masternodes And Governance'
    author:
        - 'The PIVX Team'
---

### Introduction

This tutorial will guide you through the steps necessary to setup a PIVX Masternode on a Linux Virtual Private Server (VPS) that is controlled via your local Control wallet.

Setting up a PIVX masternode requires two separate core wallets:  
* 1 core wallet containing the 10,000 PIV that are locked as collateral for operating the masternode.
* 1 core wallet running the masternode itself. It must be kept online 24/7 (see additional requirements below).

The collateral wallet can be kept offline and still receive masternode payments. 

!!! NOTE If you need any additional help, feel free to join the [PIVX Discord](https://discord.pivx.org) and ask for a help in the #support channel.

!! **Stay safe on Discord!** DO NOT receive any help or assistance through private messages. There are many impersonators pretending to be PIVX team members that are trying to steal your PIVs! They might look legit, but it’s highly likely they are scammers. **__The PIVX team will never contact you privately and offer help__**. All help and advice will only be offered in the public support channel.  


### Basic requirements:

* Collateral Wallet:
  * It can be any computer running the PIVX core wallet. It will run the Control wallet and hold the masternode coins.
  * The collateral wallet needs to hold 10,000 PIV 
  
* Masternode server:
  * Remote VPS with an OS supporting PIVX Core Wallet installed, with a fixed IP address and running 24/7
  * Minimum VPS specs: 50 GB of storage space, 2 GB of RAM, 1 dedicated CPU core
  * The latest PIVX Core wallet release installed on the masternode

!! NOTE: You will need a different IP address for each masternode you plan to host. 

### Configuration of Your Control Wallet

[plugin:youtube](https://www.youtube.com/embed/lu30liuu-lU)


#### Step 1 – Download the PIVX Wallet


Download the most recent version of the PIVX Core wallet here:

https://github.com/PIVX-Project/PIVX/releases/latest


#### Step 2 – Install the Wallet

Installation varies based on OS, please see this [document](https://docs.pivx.org/wallets/pivx-core-wallet/installing-the-pivx-core-wallet#installation) for installation assistance. Linux users, please note there are additional installation steps during initial installation. After starting the wallet for the first time, it will offer you to make a default PIVX data directory.  

* Windows: %appdata%/pivx
* Linux: ~/.pivx
* MacOS: ~/Library/Application Support/PIVX

If you choose your own location ensure that you record where that is.


#### Step 3A – Create a Masternode Using Creation Wizard

First of all, make sure that you have 10,000 PIV in your wallet.  

1. Unlock the wallet
2. Go to “Masternodes” tab
3. Click “Create Masternode Controller“
![masternode-Tutorial1](1_masternode_tab.png?classes=center,img-fluid,py-4)

4. Masternode Creation Wizard intro window will open. It just reminds you that you need to have 10,000 PIV in your wallet in order to create a Masternode. Just click the “Next” button.
![masternode-Tutorial2](2_Recommendations.png?classes=center,img-fluid,py-4)

5. Now you need to type the Masternode name as per your wish (i.e. “Masternode01”) and then click “Next” button again.
![masternode-Tutorial3](3_name_your_masternode.png?classes=center,img-fluid,py-4)

6. You will be asked to type the IP address of your VPS (it might look similar to “182.214.90.12”), and then click “Next” button again.
![masternode-Tutorial4](4_IP_and_port.png?classes=center,img-fluid,py-4)

7. If everything was successful, you should get a message “Masternode created!”.
![masternode-Tutorial5](5_masternode_created.png?classes=center,img-fluid,py-4)

8. Status of the newly created Masternode will be “MISSING”. That is normal in this phase.
![masternode-Tutorial5](6_masternode_missing.png?classes=center,img-fluid,py-4)


#### Step 3B - Create a Masternode Using the Command Line

1. Download the latest PIVX wallet release (Skip if you already have it installed)
```
	cd ~ && wget https://github.com/PIVX-Project/PIVX/releases/download/v[version]/pivx-[version]-x86_64-linux-gnu.tar.gz
	tar -zxvf pivx-[version]-x86_64-linux-gnu.tar.gz && sudo rm -f pivx-[version]-x86_64-linux-gnu.tar.gz
	cd ~/pivx-[version]/ && ./install-params.sh
```
2. Open your PIVX wallet and let it sync (Skip if you already have it installed and synchronized)
```
	cd ~/pivx-[version]/bin && ./pivxd -daemon
```
3. Generate a new PIVX address and send exactly 10K PIVX to it
```	
	./pivx-cli getnewaddress
```	
If you are sending from within this wallet to the new address then run this command:
```	
	./pivx-cli sendtoaddress ADDRESSfromGETNEWADDRESS 10000
```
4. Get the masternode private key and masternode outputs, Save them to a text document for the upcoming steps:
```
	./pivx-cli createmasternodekey
	./pivx-cli getmasternodeoutputs
```

	You can now close your PIVX Control wallet by running the following command:
```
	./pivx-cli stop
```

5. We need to now add the information above to our "Masternode.conf file"
```
	cd ~/.pivx
```
Open masternode.conf with your favorite text editor and add in the following:
```
	{Name of Masternode} {VPS IP Address}:51472 {The result of createmasternodekey you saved in the text doc.} {Result of the getmasternodeoutputs} {The Single Digit Number after Masternode Ouputs}
```
Sample Input:
```
	mn1 127.0.0.2:51472 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0
```

** We will get back here to Control wallet little bit later after we setup VPS. **

### VPS Remote Wallet Installation

These procedures are for a clean server install. If you have an existing installation then some steps may not be required. Performing the steps is unlikely to have any effect on the system. Securing the server has NOT been included in this tutorial. That is your responsibility. Although it’s not required, a great guide can be found on this [Digital Ocean](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04) tutorial.  

To be able to access a VPS, you need a software/SSH client like [PuTTY](https://www.putty.org/) for example. You can choose between alternatives as well, but this tutorial will not include installation of such software. After you successfully login to your VPS, follow these steps:  

#### Step 1 – Install Most Recent Security Patches

A clean server install will likely need some software updates. Enter the following command which will bring the system up to date:  

```
    sudo apt-get update && sudo apt-get -y upgrade
```

#### Step 2 – Download and Extract PIVX Core Wallet for Linux

Enter the following command lines one by one to download and extract PIVX wallet:
```
cd ~ && wget https://github.com/PIVX-Project/PIVX/releases/download/v[version]/pivx-[version]-x86_64-linux-gnu.tar.gz

tar -zxvf pivx-[version]-x86_64-linux-gnu.tar.gz && sudo rm -f pivx-[version]-x86_64-linux-gnu.tar.gz
```

#### Step 3 – Create the Masternode Configuration File and Populate

Before the node can operate as a masternode a custom configuration file needs to be created. Since we have not loaded the wallet yet, we will create the necessary directories and the configuration file by typing the following command lines one by one:  

```
mkdir ~/.pivx && cd ~/.pivx && sudo apt-get install nano && touch pivx.conf && nano pivx.conf
```
This command has created a blank PIVX configuration file where we will enter our masternode configuration variables. Now we should properly setup configuration settings.  

Paste the following configuration settings into the editor (using PuTTY, paste is being done simply by right mouse click):
```
rpcuser=<YOUR_OWN_RPC_USERNAME>
rpcpassword=<YOUR_OWN_RPC_PASSWORD>
rpcallowip=127.0.0.1
server=1
daemon=1
maxconnections=256
```

Before you exit the editor, there are a few parameters that you need to update with your own settings. These are:  

 * <YOUR\_OWN\_RPC\_USERNAME\> – Set this to a custom username. i.e. rpcuser.
 * <YOUR\_OWN\_RPC\_PASSWORD\> – Set this to a STRONG password. i.e. password<– NO!!! Use something more complex for your own safety!
* Go back to the Control wallet Masternode tab and click on the 3 dots next to the Masternode you created a few steps back and then click “Info“.

![masternode-Tutorial6](7_Start.png?classes=center,img-fluid,py-4)

* Now click the icon next to “Export data to run the Masternode on a remote server“.  
![masternode-Tut1](9_export_configuration.png?classes=center&resize=480)  

* It will now ask you for a confirmation to export the required data to run a Masternode. Click “OK” button.  
![masternode-Tut2](10.confirm_export_config.png?classes=center&resize=480)  

* Now you will get a message that required info was successfully exported (copied to your clipboard) and now you should paste it in your pivx.conf file on your VPS under themaxconnections=256 line in pivx.conf file.  
![masternode-Tut3](11.confirm_export_config2.png?classes=center,img-fluid,py-4)  

* When done, your pivx.conf file on your VPS should look like the following:  

```
rpcuser=root
rpcpassword=PasswordOfYourChoice
rpcallowip=127.0.0.1
server=1
daemon=1
maxconnections=256
masternode=1
externalip=101.168.87.207
masternodeaddr=101.168.87.207:51472
 masternodeprivkey=87haGjw6ABVZfZTcMNX5c1E3HUVH4qWcdc823RBDHsGC5P8FohW
```

Save and exit the editor by pressing CTRL-O and Enter to save and CTRL-X to exit the editor.

### Start Your Masternode

#### Step 4 – Load the Masternode

With the configuration created we are now ready to load the masternode and sync to the network. Load the masternode by typing the following command:  
```
        cd ~ && cd ~/pivx-[version]/bin && ./pivxd
```
You will get the message “PIVX server starting”. To follow the progress until the wallet is fully loaded and synchronized, type:

        tail -f ~/.pivx/debug.log

Wait until you see the message similar to the following:

    2020-01-10 13:31:01 CMasternodeSync::GetNextAsset – Sync has finished
    2020-01-10 13:31:01 CActiveMasternode::ManageStatus() – not capable: Hot node, waiting for remote activation.

Once you get this message, you are completely synced and masternode is ready to be started. PressCTRL-C to get back to command line.
________________________________________________________________________________________________________________
EXTRA STEP ONLY IF YOU DON’T SEE THESE 2 LINES/MESSAGES ANYWHERE:

        ./pivx-cli getbestblockhash

You will get back hash that will look like this:

    1ab2a12a1a1a121a1212ab1aba121212121ab1a1a12a12121aba1a1abab1212aa1
    
Paste the number you get after./pivx-cli reconsiderblockcommand like this:

        ./pivx-cli reconsiderblock 1ab2a12a1a1a121a1212ab1aba121212121ab1a1a12a12121aba1a1abab1212aa1

Finally, type:

        ./pivx-cli clearbanned

________________________________________________________________________________________________________________
NOTE: Wait for 15 confirmations on the blockchain for transaction with the masternode collateral before proceeding with the next steps below.

Now go back to your Control wallet -> Masternodes -> Click “Start Inactive/s”
Status will change from MISSING -> PRE_ENABLED.
![masternode-Tut3](12.pre_enabled.png?classes=center,img-fluid,py-4)

** From the command line: **
If you have a password set on your wallet you will first need to unlock it (90 means it will be unlocked for 90 seconds):
```
./pivx-cli walletpassphrase YOURPASSWORD 90
```

You can now proceed to start your masternode:
```
startmasternode missing y
```

If everything went well, you should receive the message: "Masternode successfully started"

**Congratulations!** You have successfully started your masternode!

ADDITIONAL NOTES:

1. If the output of getmasternodestatus is fine, then you are perfectly fine. But have in mind that it can take up to 2 hours for masternode to change status from PRE_ENABLED to ENABLED in the masternode list.

2. First masternode reward requires a longer waiting period. It usually takes 3-5 days to receive a first masternode reward.

3. You can close the Control wallet, as it is not needed. Only the VPS should be working 24/7.

!!! If you have any troubles or issues, feel free to join [PIVX Discord](https://discord.pivx.org/) and post your questions in the **#support** channel.  

!! **Stay safe on Discord!** DO NOT receive any help or assistance through private messages. There are many impersonators pretending to be PIVX team members that are trying to steal your PIVs! They might look legit, but it’s highly likely they are scammers. **__The PIVX team will never contact you privately and offer help__**. All help and advice will only be offered in the public support channel.  

### Shutting Down a Masternode

How do I stop a running masternode on my VPS and delete masternode from my PIVX Control wallet?  
1. In Control wallets Masternode tab click on the Masternode you wish to shutdown and click “Delete”.
2. Restart the wallet.
3. Your 10,000 coins are now unlocked and spendable.


How do I get the 10,000 PIVX back that I’ve send to my Masternode address at the beginning?  
* You don’t need to “get it back” as it is already in your wallet.
* Being in the different address is not an issue as that’s also your address.

Can I use the 10,000 PIVX normally on my wallet, sell it or stake it like before?  
* Yes! If your wallet is unlocked for staking, it will automatically stake these 10,000 coins and you can spend them at any time.  
