---
title: 'Run PIVX Core Wallet as a service on Linux'
image: troubleshooting.png
taxonomy:
    category:
        - 'Knowledge Base'
    author:
        - 'The PIVX Team'
---

The PIVX Core Wallet can be setup as a service on Linux to start automatically when the server starts.

1. Create the service definition file as `/lib/systemd/system/pivxd.service`
2. Put the following content in the file. Make sure you customize the user (set to `pivx-user` in the example below, and the path to the `pivxd` binary)
```
# It is not recommended to modify this file in-place, because it will
# be overwritten during package upgrades. If you want to add further
# options or overwrite existing ones then use
# $ systemctl edit pivxd.service
# See "man systemd.service" for details.
#
# Note that almost all daemon options could be specified in
# /home/pivx-user/.pivx/pivx.conf
#
[Unit]
Description=PIVX daemon
After=network.target
Documentation=man:pivxd(1)
#
[Service]
ExecStart=/home/pivx-user/pivx-core/bin/pivxd -daemon -datadir=/home/pivx-user/.pivx -conf=/home/pivx-user/.pivx/pivx.conf -pid=/run/pivxd/pivxd.pid
# Creates /run/pivxd owned by pivx-user
RuntimeDirectory=pivxd
User=pivx-user
Type=forking
PIDFile=/run/pivxd/pivxd.pid
Restart=on-failure
#
# Hardening measures
####################
#
# Provide a private /tmp and /var/tmp.
PrivateTmp=true
#
# Mount /usr, /boot/ and /etc read-only for the process.
ProtectSystem=full
#
# Disallow the process and all of its children to gain
# new privileges through execve().
NoNewPrivileges=true
#
# Use a new /dev namespace only populated with API pseudo devices
# such as /dev/null, /dev/zero and /dev/random.
PrivateDevices=true
#
# Deny the creation of writable and executable memory mappings.
MemoryDenyWriteExecute=true
#
[Install]
WantedBy=multi-user.target
```

3. Update systemd configuration:
```
sudo systemctl daemon-reload
```

4. Start the service
```
sudo systemctl start pivxd
```

5. You can check the status with:
```
sudo systemctl status pivxd
```

6. If successful enable for system startup:
```
sudo systemctl enable pivxd
```

