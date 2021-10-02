# VPN

## VPN PPTP (Point to Point Tunneling Protocol)

128bit  weak and DEPRECATED...

tcp 1723
upd 47

PPTP (RRAS)

## VPN L2TP (Level 2 Tunneling Protocol)

256bit

udp 1701
--
tcp 1701
udp 500, 4500

the router must to have passthrough and port forwarding

## SSTP (Secure Socket Tunneling Protocol)

256bit
tcp 443

## IpeSec IKEv2

udp 500, 4500

RRAS

## OpenVPN

udp 1194




## Tooling


### openVPN

```bash
sudo su
apt-get install openvpn easy-rsa -y
```

### fortinet VPN

```
sudo dnf install openvpn openfortivpn  NetworkManager-fortisslvpn-gnome

sudo apt install network-manager-fortisslvpn-gnome

snap search openforivpn
```


default ports:

```
8900 TCP
10443
```

The default SSL VPN port is either 443 or 10443 on the FortiGate.

VPN settings distribution to authenticated FortiClient installations See originating port TCP 8900.	TCP 8900
SSL VPN	TCP 10443

```
sudo cat /etc/openfortivpn/config


host = your.fortivpnserver.com
port = 10443
username = john.doe
password = passwd123
```



scan if port is open
```
nmap –p 80-1080 192.168.0.1
```


### strongswan : An OpenSource IPsec-based VPN and TNC solution

strongwan A popular open source Linux implementation of IPsec ipsec.conf


```bash
sudo dnf strongswan strongswan-libipsec NetworkManager-strongswan-gnome NetworkManager-strongswan


connect to fortigate using strongswan


conn fortinet
left=%any
leftauth=psk
leftid=""
leftauth2=xauth
xauth_identity="your_username"
leftsourceip=
```

### fortinet (official)

note: linux client don't support IpSec


https://repo.fortinet.com/

```bash
# 6.0 version
# - crash in fedora 33
sudo dnf config-manager --add-repo  https://repo.fortinet.com/repo/centos/7/os/x86_64/fortinet.repo

# 6.4
# don't have options for IPSec
sudo dnf config-manager --add-repo https://repo.fortinet.com/repo/6.4/centos/7/os/x86_64/fortinet.repo

# 7.0
# don't have options for IPSec
sudo dnf config-manager --add-repo  https://repo.fortinet.com/repo/7.0/centos/8/os/x86_64/fortinet.repo



sudo dnf install forticlient
```


### l2tp

```bash
sudo dnf install NetworkManager-l2tp NetworkManager-l2tp-gnome

```


### libreswan


```bash
sudo dnf install NetworkManager-libreswan NetworkManager-libreswan-gnome

/etc/swanctl/config.d/name-it-your-vpn.conf
```
