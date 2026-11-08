# Reconnaissance & Scanning Phase

In this phase, we seek to gather as much information prior to attacking the target. The goal is to map our attack surface and identify any weakpoints that we can leverage.

## Reconnaissance
### WHOIS
**cmd used:**
`whois [IP Address of Target Machine]`

**Result**
I found out that the IP address is owned by the Internet Assigned Numbers Authority (IANA). From here I can get the address of the registered company and abuse contact to gives myself a foot in the door.

### DIG / NSLOOKUP
**cmd used:**
`dig [IP]` and `nslookup [domain]`

**Result**
Due to the victim machine being connected via Host only, these options did nothing. Due to it being hosted on a private network without access to the internet there would be nothing to report. However, these are important tools to figure out network structure. 



## Scanning The Target
Using Nmap 7.99 we scanned our victim machine for open ports and services. The following chart demonstrates the results.
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