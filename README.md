# IMSI-Catcher
This program show you IMSI numbers of cellphones around you.

Description: 

The IMSI catcher uses a famous technique called man-in-the-middle (MITM) attack. It acts simultaneously as a fake mobile phone to the real base station and a fake base station to the real mobile phone 

    
⚠️ This program was made to understand how GSM network work. Not for bad hacking ! ⚠️


## Setup

```bash
git clone https://github.com/Oros42/IMSI-catcher.git
cd IMSI-catcher
```
or
```bash
wget https://github.com/Oros42/IMSI-catcher/archive/master.zip && unzip -q master.zip
cd IMSI-catcher-master
```
  
```bash
sudo apt install python3-numpy python3-scipy python3-scapy
```
Warning : don't use python 3.9 (ctypes bug)!  




## Usage

We use `grgsm_livemon` to decode GSM signals and `simple_IMSI-catcher.py` to find IMSIs.  
  
```bash
python3 simple_IMSI-catcher.py -h
```
```
Usage: simple_IMSI-catcher.py: [options]

Options:
  -h, --help            show this help message and exit
  -a, --alltmsi         Show TMSI who haven't got IMSI (default  : false)
  -i IFACE, --iface=IFACE
                        Interface (default : lo)
  -m IMSI, --imsi=IMSI  IMSI to track (default : None, Example:
                        123456789101112 or "123 45 6789101112")
  -p PORT, --port=PORT  Port (default : 4729)
  -s, --sniff           sniff on interface instead of listening on port
                        (require root/suid access)
  -w SQLITE, --sqlite=SQLITE
                        Save observed IMSI values to specified SQLite file
  -t TXT, --txt=TXT     Save observed IMSI values to specified TXT file
  -z, --mysql           Save observed IMSI values to specified MYSQL DB (copy
                        .env.dist to .env and edit it)
```

## What you need

1 PC with Gnu/Linux. Tested with :  
- debian 10  
- Ubuntu 20.04/LinuxMint 20+  
- Kali 2020+  
  
1 SDR receiver. Tested with :  
- [USB DVB-T key (RTL2832U)](https://osmocom.org/projects/sdr/wiki/rtl-sdr) with antenna (less than 15$)  
- [OsmocomBB phone](https://osmocom.org/projects/baseband/wiki/Phones)  
- [HackRF](https://greatscottgadgets.com/hackrf/)  
- [BladeRF](https://www.nuand.com/bladerf-2-0-micro/)

Open 2 terminals.  
  
In terminal 1  
```bash
sudo python3 simple_IMSI-catcher.py -s
```
  
In terminal 2  
```bash
grgsm_livemon
```
Now, change the frequency until it display, in terminal, something like that :  
``` 
15 06 21 00 01 f0 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b
25 06 21 00 05 f4 f8 68 03 26 23 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b
49 06 1b 95 cc 02 f8 02 01 9c c8 03 1e 57 a5 01 79 00 00 1c 13 2b 2b
```

### Wireshark

You can watch GSM packets with wireshark.  
```bash
sudo apt install wireshark
sudo wireshark -k -Y '!icmp && gsmtap' -i lo
```

### Find frequencies
 
```bash
grgsm_scanner
```
```
ARFCN:  974, Freq:  925.0M, CID:     2, LAC:   1337, MCC: 208, MNC:  20, Pwr: -41
ARFCN:  976, Freq:  925.4M, CID:  4242, LAC:   1007, MCC: 208, MNC:  20, Pwr: -45
```
Now, you can set the frequency for `grgsm_livemon` :  
```bash
grgsm_livemon -f 925.4M
