# azfw-search

### azfw-search - search rules in Azure Firewall Service 

requrements:

- python3
- json file 


## instalation 

```
get clone https://github.com/ruslansvs2/azfwsearchrules.git

pip3 install json argparse ipaddress

#or
# for RedHat 
yum -y install python3-json python3-argparse python3-json python3-ipaddress
# for Debian like destributuions 
apt -y install python3-json python3-argparse python3-json python3-ipaddress


cd azfwsearchrules; cp azfs-search /usr/sbin/


```

## how to use 

1. create json file 

```
az login

az network firewall network-rule collection list -g GroupName   -f FirewallName > fwdata.json


```

2. Help

print help instruction 

```
./azfw-search -h
usage: azfw-search.py [-h] [-s SOURCE_IP] [-d DESTANATION_IP] [-p DESTANATION_PORT] [-P PROTOCOL] [-f FILE] [-tag TAG]

optional arguments:
  -h, --help            show this help message and exit
  -s SOURCE_IP, --source-ip SOURCE_IP
                        A source IP address
  -d DESTANATION_IP, --destanation-ip DESTANATION_IP
                        A destanation IP address
  -p DESTANATION_PORT, --destanation-port DESTANATION_PORT
                        A destanation port
  -P PROTOCOL, -proto PROTOCOL, --protocol PROTOCOL
                        protocol
  -f FILE, --file FILE  A data file, the default file is fwdata.json
  -tag TAG, --tag TAG   Service tags, example: -tag yes

```

3. Search rule(s)


```
./azfw-search -f fwdata.json  -p 443 -s 192.168.0.30
===========================

Set of Rules:  ActiveDirectory
Source IP:   192.168.0.0/16
Destination IP:  *
Destination PORT:  123 389 135-139 443 636 445
Protocol:  UDP TCP


===========================

Set of Rules:  WEB
Source IP:   192.168.0.0/24
Destination IP:  10.0.0.0/20
Destination PORT:  80 443
Protocol:  TCP


```


