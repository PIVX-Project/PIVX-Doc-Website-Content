---
title: 'Setting up a PIVX Wallet/Masternode behind Tor'
taxonomy:
    category:
        - 'Knowledge Base'
    author:
        - 'The PIVX Team'
---

!! NOTE: Starting with version 5.3.0, PIVX Core only supports Tor version 3 hidden services (Tor v3). Tor v2 addresses are ignored by PIVX Core and neither relayed nor stored.

## Install & configure Tor on your system:

1. Install Tor according on the computer/serveur running the core wallet using the official Tor instructions: https://community.torproject.org/onion-services/setup/install/

2. Create a dedicated Tor service:
```
	tor-instance-create 00
```
3. Activate the service and disable the default Tor service (if not required for other purposes):
```
systemctl enable tor@00
systemctl mask tor@default
```
4. Configure Tor instance (paste the below in ```/etc/tor/instances/00/torrc```):
```
# This is the tor configuration file for tor instance 00.
#
# To start/reload/etc this instance, run "systemctl start tor@00" (or reload, or..).
# This instance will run as user _tor-00; its data directory is /var/lib/tor-instances/00.
#
# Append to the list of socks interfaces configured via
# /usr/share/tor/tor-service-defaults-torrc-instances
# which is unix:/run/tor-instances/00/socks
#
# This is the tor configuration file for tor instance 00.
#
# To start/reload/etc this instance, run "systemctl start tor@00" (or reload, or..).
# This instance will run as user _tor-00; its data directory is /var/lib/tor-instances/00.
#
## ControlPort and authentication cookie for tor-arm, nyx, pivxd
## Start nyx: ~$ nyx -i 9051
## Hint: alias to user's .bashrc ( alias nyx00='nyx -i 9051' )
ControlPort 9051
#CookieAuthentication 1
#
## Tor opens a socks proxy on port 9050 by default -- even if you don't configure one below.
SocksPort 9050
## SocksPort flag: OnionTrafficOnly
## Tell the tor client to only connect to .onion addresses in response to SOCKS5 requests on this connection.
## This is equivalent to NoDNSRequest, NoIPv4Traffic, NoIPv6Traffic.
#SocksPort 9050 OnionTrafficOnly
#
## Entry policies to allow/deny SOCKS requests based on IP address.
## First entry that matches wins. If no SocksPolicy is set, we accept
## all (and only) requests that reach a SocksPort. Untrusted users who
## can access your SocksPort may be able to learn about the connections
## you make.
SocksPolicy accept 127.0.0.1
SocksPolicy reject *
#
## Tor will reject application connections that use unsafe variants of the socks protocol
## -- ones that only provide an IP address, meaning the application is doing a DNS resolve first.
## Specifically, these are socks4 and socks5 when not doing remote DNS.
#SafeSocks 1
#
## Tor will make a notice-level log entry for each connection to the Socks port indicating
## whether the request used a safe socks protocol or an unsafe one (see above entry on SafeSocks).
## This helps to determine whether an application using Tor is possibly leaking DNS requests.
#TestSocks 1
#
## A list of preferred nodes to use for the first hop in the circuit, if possible.
#EntryNodes $fingerprint,$fingerprint,...
## A list of preferred nodes to use for the last hop in the circuit, if possible. (Hint: OnionTraffic don't exit Tor network)
#ExitNodes $fingerprint,$fingerprint,...
## A list of nodes to never use when building a circuit.
#ExcludeNodes Unnamed,default
## A list of nodes to never use when picking an exit. Nodes listed in ExcludeNodes are automatically in this list.
#ExcludeExitNodes $fingerprint,$fingerprint,..
#StrictNodes 1
#
#ClientUseIPv6 1
LongLivedPorts 51472
# Default: 21, 22, 706, 1863, 5050, 5190, 5222, 5223, 6523, 6667, 6697, 8300 
```
5. Start the Tor service:
```
systemctl start tor@00
```
6. Check whether it's running:
```
systemctl status _tor@00
```

7.  Add both the user running Tor and the user running pivxd (pivx in the example below) to the same group, so that pivxd has the rights to use the Tor control port & can assess the authentication cookies:
```
usermod -aG _tor-00 pivx
```

!! NOTE: It is recommended to setup the core wallet to communicate through the Tor network only when the blockchain is completely synchronized. The Tor network is slower, and a full blockchain sync creates unnecessary Tor traffic. All Tor relays are privately funded not by the Tor Project!

## Now head over to the PIVX Core Wallet and configure it as below:

8. To connect the pivxd wallet via the Tor network, you can either:
	1. add the following flags to the pivxd command upon startup and restart the PIVX Core wallet:
```
-proxy=127.0.0.1:9050 -listen
```
	2. or add the following command line in the pivx.conf file and restart the PIVX Core wallet:
```
# Connect via a SOCKS5 proxy (default: 127.0.0.1:9050)
proxy=127.0.0.1:9050
# Tor control port to use if onion listening enabled (default: 127.0.0.1:9051)
torcontrol=127.0.0.1:9051
#
# Listening mode, enabled by default except when 'connect' is being used
listen=1
```

## Verify that your Core Wallet is properly connected via Tor:

This is done by running `pivx-cli getnetworkinfopivx-cli getnetworkinfo`. Your Onion service address should appear in the result:
```
"localaddresses": [
{
  "address": "oe3h23q27lrc2xuojakh76ntq3ht3ew5mfnwu3ag2vgfq5hwynewvdad.onion",
  "port": 51472,
  "score": 4
}
```

This is also visible in the debug.log with a line like this one:

`2021-11-06T19:08:18Z tor: Got service ID oe3h23q27lrc2xuojakh76ntq3ht3ew5mfnwu3ag2vgfq5hwynewvdad, advertising service oe3h23q27lrc2xuojakh76ntq3ht3ew5mfnwu3ag2vgfq5hwynewvdad.onion:51472`

And in the GUI via the Tor icon on the main screen:
![1.tor_active](1.tor_active.png?classes=center&resize=600)

## If you are configuring a masternode wallet to run behind Tor:

1. Stop Masternode Hot Wallet
2. Delete onion_v3_private_key file in PIVX data directory if it exists (so the wallet could get a v3 address - it was previously using a v2 address named that per the release notes of version 5.3)
3. Comment out the following lines in hot wallet pivx.conf: masternode=1, masternodeaddr, masternodeprivkey - this is so that the wallet doesn't quit when starting and gets a new v3 private key.
4. Start Masternode Hot Wallet
5. check debug.conf for new .onion address - you can find it by searching for this string "tor: Got service ID"
6. Stop hot wallet.
7. Edit hot wallet pivx.conf masternodeaddr line to equal the address from step 5. Uncomment all lines commented out in step 3.
  ```
  # replace with 'your .onion address' 🔻
  externalip=oe3h23q27lrc2xuojakh76ntq3ht3ew5mfnwu3ag2vgfq5hwynewvdad.onion
  #	
  # Masternode options:
  #
  masternode=1
  masternodeaddr=oe3h23q27lrc2xuojakh76ntq3ht3ew5mfnwu3ag2vgfq5hwynewvdad.onion
  masternodeprivkey=91v..............................................8K
  ```
8. Start hot wallet
9. Edit masternode.conf on CONTROLLER (cold wallet) to insert new address from step 5.
10. Start controller wallet and let it synch
11. Restart masternode.
12. Shut down cold wallet
13. Check masternode wallet status using `pivx-cli getmasternodestatus`


!! NOTE: More detailed instructions/details on the various configuration options are also available at https://github.com/PIVX-Project/PIVX/blob/master/doc/tor.md
