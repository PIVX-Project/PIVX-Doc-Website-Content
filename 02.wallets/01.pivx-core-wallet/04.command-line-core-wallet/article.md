---
title: 'PIVX Command Line Core Wallet'
taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

The process to launch the PIVX Core Wallet in command line is called **pivxd** and can be found in the bin folder of the pivx core wallet.  

The base command to launch the pivx core wallet is:  

`pivx-[version]/bin/pivxd -daemon`

The **pivxd** process accepts multiple command line options that can be listed (along with their description) using the following command:  

`pivxd --help`  

When no options are specified, the **pivxd** process will use default values for all parameters (such as data folder, log file, etc.), or the ones specified in the pivx.conf file.  

The **pivxd** server logs all of its activities in the `$PIVX_HOME/debug.log` file.  

### Starting the pivxd Process Automatically When the Server Starts

1. Create a service file
  * `sudo nano /etc/systemd/system/PIVX.service`

2. Copy the following to the newly created PIVX.service file. You may need to adjust the wallet version, the path to PIVX bin folder, and your username:  

```
[Unit]
Description=PIVX_MN
After=network.target [Service]
User=piv
ExecStart=/home/piv/pivx-[version]/bin/./pivxd -daemon
ExecStop=/home/piv/pivx-[version]/bin/./pivx-cli stop
TimeoutSec=15min
Type=forking
Restart=on-failure
PrivateTmp=true
ProtectSystem=full
NoNewPrivileges=true
PrivateDevices=true
[Install]
WantedBy=default.target
```

3. Activate the service with this command:  
  * `sudo systemctl enable PIVX`

3. Start the service:
  * `sudo systemctl start PIVX`

### Client Process

The process to access the PIVX Core Wallet in command line is called **pivx-cli** and can also be found in the bin folder of the pivx core wallet.  
The following command lists all the available command line options:

`pivx-[version]/bin/./pivx-cli help`

The `help` function can also be used to get help on a particular command. For example the following returns instructions and examples for the **getinfo** command:

`pivx-[version]/bin/./pivx-cli help getinfo`
	
### Useful Commands

* **pivx-cli walletpassphrase MyPassPhrase 999**: unlocks the wallet for 999 seconds (for spending and staking)
* **pivx-cli walletpassphrase MyPassPhrase 9999999 true**: unlocks the wallet for 9999999 seconds (for staking only)
* **pivx-cli getstakingstatus**: Displays all details pertaining to staking (helpful to debug staking issues)
* **pivx-cli sendtoaddress "DMJRSsuU9zfyrvxVaAEFQqK4MxZg6vgeS6" 1.5**: Sends 1.5 PIV to address DMJRSsuU9zfyrvxVaAEFQqK4MxZg6vgeS6

	
	
	
	
