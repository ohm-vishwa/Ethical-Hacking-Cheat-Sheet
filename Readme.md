# <p style="text-align:center">Ethical Hacking Cheat Sheet </p>
<details>
    <summary> Basic Information</summary>
These commands are works only on linux based OS system
An external Network Adapter is required, Your Network Adapter must support
{ Monitor Mode, packet injection } mode Here my network interface name is { wlan1 }, use these commands 

```sh
iwconfig 
```
 or 
 ```
 ifconfig
 ```
check your network interface name, your network interface name may be diffrent use accordingly.

First you need to switch root user

```
sudo su
```
</details>

# Table of Content
- [Network Manager Commands](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#network-manager-commands)
- [Network Adapter testing commands](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#network-adapter-testing-commands)
- [Packet Sniffing](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#packet-sniffing)
- [DE-Authentication Attack](https://github.com/ohm-vishwa/Ethical_Hacking?tab=readme-ov-file#de-authentication-attack)

---
## Network Manager Commands
### Kill Network Manager
```
airmon-ng check kill
```
### Enable Network Manager
```
service NetworkManager start
```
### Restart Network Manager
```
systemctl restart NetworkManager
```
### Check Status of Network Manager
```
systemctl status NetworkManager
```
---
## Network Adapter Testing Commands
### Enable Monitor Mode
```
airmon-ng start wlan1
```
### Disable Monitor Mode
```
airmon-ng stop wlan1
```
### Packet Injection test
```
aireplay-ng --test wlan1
```
### Creating Access Point Test
you can put any fake MAC Address like this `00:01:02:03:04:05`
```
airbase-ng -a 00:01:02:03:04:05 --essid "test_01" -c 11 wlan1
```
---
## Packet Sniffing
<details>
    <summary>What is Packet Sniffing ?</summary>
Packet sniffing is like secretly listening to conversations on the internet to see what information is being sent between computers.
</details>

### Sniff Network around `2.4 GHz`
```
airodump-ng wlan1
```
### Sniff Network Both `2.4 GHz and 5 GHz`
```
airodump-ng --band a wlan1
```
### Capture data both `2.4 GHz and 5 GHz`
```
airodump-ng --band abg wlan1
```
### Capture data in a file `test`
```
airodump-ng --bssid @1 --channel @2 --write test wlan1
```
@1 → `BSSID` of target

@2 → Channel no. of target

### Open wireshark application to read captured data, captured in `fileName.cap`, 
```
wireshark
```
---
## DE-Authentication Attack 
<details>
    <summary>why de-authentication attack ?</summary>
it`s cool and amazing attack on your nearest routers  & devices, it uses { aireplay } package and takes MAC address of Router & Client and keep sending deauthentication packet to Router & Client as well, you can send really large no. of packets and keep client disconnect as you want.
</details>

```
aireplay-ng --deauth @1 -a @2 -c @3 wlan1
```
@1 → no. of packets you want to send 

@2 → BSSID of router

@3 → MAC Address of the Client

&nbsp;

if it`s fails then, target router on specfic channel
```
airodump-ng --bssid @1 --channel @2 wlan1
```
@1 → BSSID of target

@2 → Channel number



# ===}> [Keep Supporting me on YouTube](https://www.youtube.com/@ohm_vishwa)