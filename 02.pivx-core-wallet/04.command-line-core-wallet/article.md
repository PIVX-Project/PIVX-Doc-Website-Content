---
title: 'PIVX Command Line Core Wallet'

taxonomy:
    category:
        - 'PIVX Core Wallet'
    author:
        - 'The PIVX Team'
---

### Description of the pivxd Server Process

The process to launch the PIVX Core Wallet in command line is called pivxd and can be found in the bin folder of the pivx core wallet.

The base command to launch the pivx core wallet is:

	pivx-5.3.0/bin/pivxd -daemon

The pivxd process accepts multiple command line options, that can be listed (along with their description) using the following command:

	pivxd --help

When no options are specified, the pivxd process will use default values for all parameters (such as date folder, log file, etc.), or the ones specified in the pivx.conf file.

The pivxd server logs all its activities in the following file:

	$PIVX_HOME/debug.log

### Start the pivxd process automatically when the server starts

1. Create a service file

	sudo nano /etc/systemd/system/PIVX.service

2. Copy the following to the newly created PIVX.service file. The elements in purple are to be modified according to the version of PIVX, your path, and your username:

```
[Unit]
Description=PIVX_MN
After=network.target [Service]
User=piv
ExecStart=/home/piv/pivx-5.3.2/bin/./pivxd -daemon
ExecStop=/home/piv/pivx-5.3.2/bin/./pivx-cli stop
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

3. Activate the service

```
sudo systemctl enable PIVX
```

3. Start it

```
sudo systemctl start PIVX
```

### Client Process

The process to access the PIVX Core Wallet in command line is called pivx-cli and can be found in the bin folder of the pivx core wallet.

The following command line lists all the available options, sorted by theme:

	pivx-5.3.0/bin/pivx-cli help

The help function can also be used to access the documentation page for a particular command line option. For example the following returns the help page for the **getinfo** command:

	pivx-5.3.0/bin/pivx-cli help getinfo
	
### Useful commands

* **pivx-cli walletpassphrase MypassPhrase 999**: unlocks the wallet for 999 seconds (for spending and staking)
* **pivx-cli walletpassphrase MypassPhrase 9999999 true**: unlocks the wallet for 9999999 seconds (for staking only)
* **pivx-cli getstakingstatus**: Displays all details pertaining to staking (helpful to debug staking issues)
* **pivx-cli sendtoaddress "DMJRSsuU9zfyrvxVaAEFQqK4MxZg6vgeS6" 1.5**: Sends 1.5 PIV to address DMJRSsuU9zfyrvxVaAEFQqK4MxZg6vgeS6

	
	
	
	
