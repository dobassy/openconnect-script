# openconnect excample
It is a sample for VPN connection from macOS to [Cisco's AnyConnect SSL VPN][cisco-anyconnect] Server using OSS [openconnect][openconnect].

[cisco-anyconnect]: https://www.cisco.com/c/en/us/products/security/anyconnect-secure-mobility-client/index.html
[openconnect]: https://github.com/openconnect/openconnect "openconnect/openconnect: Mirror of the official openconnect repository"

## Installation from brew (macOS)

```
brew cask install tuntap
brew install vpnc
brew install openconnect
```

What's vpnc?

> OpenConnect just handles the communication with the VPN server; it does not know how to configure the network routing and name service on all the various operating systems that it runs on.
> 
> To set the routing and name service up, it uses an external script which is usually called vpnc-script.
> 
> via [Install a vpnc-script - OpenConnect VPN client.](http://www.infradead.org/openconnect/vpnc-script.html)

Warning

[vpnc's brew fomula is Inactive][vpnc-brew] as of August 2018. Probably source compilation is necessary.

[vpnc-brew]: http://brewformulas.org/vpnc "Vpnc — BrewFormulas"

## Setup environment

```
mv vpnc-script.sample vpnc-script
vi vpnc-script
```

## Exec coommand

```
sudo openconnect \
     --user=<youruser-id>@<company-domain-name> \
     --authgroup=<set here>     \
     --script=~/path/to/vpnc-script \
     --no-cert-check \        # if you need to skip the cert validation.
     <vpn-server-fqdn-or-IP>
```

Or, if you want to specify a PROXY server:

```
sudo openconnect \
     --user=<youruser-id>@<company-domain-name> \
     --authgroup=<set here>     \
     --script=~/path/to/vpnc-script \
     --proxy=http://<if you use proxy> \
     <vpn-server-fqdn-or-IP>
```

## Sample Log
```
POST https://<vpn-server-fqdn-or-IP>/
Attempting to connect to proxy X.X.X.X:8080
  ...
Connected utun1 as <VPN pool ip>, using SSL
```