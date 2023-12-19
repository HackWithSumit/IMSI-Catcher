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
