# azfw-search

### azfw-search - search rules in Azure Firewall Service 
filter features:
- searching by destanation port
- searching by source/destanation IP address 
- searching by rule name sets and rule name
- searching by protocal 
- searching in network and application rule sets
- searching by service tag

requrements:

- python3
- json file 


## instalation 

```

pip3 install argparse ipaddress

#or
# for RedHat 
yum -y install python3-json python3-argparse python3-json python3-ipaddress
# for Debian like destributuions 
apt -y install python3-json python3-argparse python3-json python3-ipaddress

get clone https://github.com/ruslansvs2/AzureFirewall-SearchRules.git 
cd AzureFirewall-SearchRules; cp azfs-search /usr/bin/


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
azfw-search  -h
usage: azfw-search.py [-h] [-s SOURCE_IP] [-d DESTANATION_IP] [-p DESTANATION_PORT] [-P PROTOCOL] [-ns NAME_SET] [-n NAME]
                      [-f FILE] [-tag TAG] [-v] [-m MODULE]

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
  -ns NAME_SET, -name_set NAME_SET, --name_set NAME_SET
                        Search rule set name, put regular expression
  -n NAME, -name NAME, --name NAME
                        Search rule name, put regular expression
  -f FILE, --file FILE  A data file, the default file is fwdata.json
  -tag TAG, --tag TAG   Service tags, example: -tag yes
  -v, --version
  -m MODULE, --module MODULE
                        firewall rule collection module, flags: network (short n) and application (short a). Default value is
                        network

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


4. Search application rule sets by name
```
azfw-search  -f fwdata.app.json  -ns let -m application
===========================

Rule sets:  PLT-EG_letsencript
Rule name:  fqdn_qualys_platform: https
Source IP:   10.10.10.0/19 10.20.20.0/19
Port and Protocol:   443
Target FQDNs:  *.api.letsencrypt.org
Service tag: 


```


