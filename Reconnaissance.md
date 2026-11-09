# Reconnaissance & Scanning Phase

In this phase, we seek to gather as much information prior to attacking the target. The goal is to map our attack surface and identify any weakpoints that we can leverage.

## Reconnaissance
### WHOIS
**cmd used:**
`whois [IP Address of Target Machine]`

**Result**\
I found out that the IP address is owned by the Internet Assigned Numbers Authority (IANA). From here I can get the address of the registered company and abuse contact to gives myself a foot in the door.

### DIG / NSLOOKUP
**cmd used:**
`dig [IP]` and `nslookup [domain]`

**Result**\
Due to the victim machine being connected via Host only, these options did nothing. Due to it being hosted on a private network without access to the internet there would be nothing to report. However, these are important tools to figure out network structure. 


## Scanning
Using Nmap 7.99 we scanned our victim machine for open ports and services. The following chart demonstrates the results.
*Disclaimer: All ports scanned are **OPEN**.*

| Port | Service |
|------|---------|
| 21/tcp | ftp |
| 22/tcp | ssh |
| 23/tcp | telnet |
| 25/tcp | smtp |
| 53/tcp | domain |
| 80/tcp | http |
| 111/tcp | rpcbind |
| 139/tcp | netbios-ssn |
| 445/tcp | microsoft-ds |
| 512/tcp | exec |
| 513/tcp | login |
| 514/tcp | shell |
| 1099/tcp | rmiregistry |
| 1524/tcp | ingreslock |
| 2049/tcp | nfs |
| 2121/tcp | ccproxy-ftp |
| 3306/tcp | mysql |
| 5432/tcp | postgresql |
| 5900/tcp | vnc |
| 6000/tcp | X11 |
| 6667/tcp | irc |
|8009/tcp | ajp13 |
|8180/tcp | unknown |

23 ports were left opened. This significantly increases our attack surface and decreases our security posture. Port 22 is for SSH and leaving it open exposes a common port used in brute force attacks. Other ports may be used to establish C2 channels that are harder to detect. 

## What You're Looking At
You are looking at the results of a scan test performed by one tool, **Nmap**. The results are seperated into 3 categories and those are **port**, **status**, and **service**. In the results we omitted the **status** category since they are all **OPEN** ports. What it doesn't tell you is what these things mean, so let's do a quick breakdown.

## Ports and Services
### Port
A port is somewhat of a door number on a machine that network can be directed to. Think of it this way, you go into the office and you look for a specific room number such as Conference Room 1. Conference Room 1 would be the port number.\
### Service
A service is a program that is running on the machine that listens on a specific port to recieve and handle incoming network traffic.\
### Why it Matters?
Well a port is an open door that is assigned to specific program or service. This is a security concern. The more open doors we have the more way an attacker can try to access our system. This is why we try to limit the quantity of ports we have open. There are typically services that like to used specific ports and this can help the attacker know what service may be running on the machine, an example would be Telnet using port 23. The attacker can then execute a specific set of exploits tailored to the Telnet service.\
Essentially an open port is a pathway into your network and a service can let attackers know which exploits may be used. 