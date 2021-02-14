Security
===


##### [Shodan](https://www.shodan.io/)
```
port:502 country:"TW"
port:4840 country:"TW"
```
---

##### [Metasploit](https://www.metasploit.com/)
###### [github](https://github.com/rapid7/metasploit-framework)
```
# curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall
# chmod 755 msfinstall
# ./msfinstall
```
```
# apt-get install postgresql postgresql-contrib -y
# service --status-all
# update-rc.d postgresql enable
# msfdb init
# msfdb reinit
```
```
searchsploit(1) - Exploit Database Archive Search
```
```
# msfconsole
msf > show options
msf > db_status
msf > db_rebuild_cache
msf > search samba
msf > show options
```
```
# msfconsole
msf > use auxiliary/scanner/portscan/syn
msf > show options
msf > set RHOSTS 192.168.0.0/24
msf > set PORTS 445
msf > run
```
```
# msfconsole
msf > use scanner/smb/smb_version
msf > show options
msf > set RHOSTS 192.168.0.0/24
msf > run
```
---

##### nmap(1) - Network exploration tool and security / port scanner
```
# nmap <IP>/<Mask> -n -sP | awk '/Nmap scan report for/ {printf $5} /MAC Address:/ {print " => "$0}'
# nmap -A <IP> -d --max-rate 0.1 --max-parallelism 1 --packet-trace
# nmap -sS -sU -PN -p 1-65535 -v <IP> --packet-trace
# nmap -sU -p 1-65535 -v <IP> --packet-trace

userdb=/usr/share/nmap/nselib/data/usernames.list
passdb=/usr/share/nmap/nselib/data/passwords.list
# nmap -p 23 --script telnet-brute --script-args userdb=<fileName>,passdb=<fileName> <IP>
# nmap -p 21 --script ftp-brute --script-args userdb=<fileName>,passdb=<fileName> <IP>
# nmap -p 80 --script http-brute <IP>
# nmap -p 22 --script ssh2-enum-algos <IP> -sV

# ls -l /usr/share/nmap/scripts
# nmap --script smb-os-discovery.nse
# nmap --script-updatedb
```
```
Install Nmap Version - https://nmap.org/dist/
# nmap -V
# apt-get purge --auto-remove nmap -y
# wget https://nmap.org/dist/nmap-7.60.tgz
# tar -zxvf nmap-7.60.tgz
# cd nmap-7.60/
# ./configure
# make
# make install
# cd /usr/bin; ln -s /usr/local/bin/nmap; cd -
```
---

##### hydra(1) - a very fast network logon cracker which supports many different services
```
# apt install hydra -y

# hydra -V -f -l <UserName> -p <Password> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -l <UserName> -p <Password> <IP> <telnet|ftp|ssh|rdp>
# hydra -V -f -l <UserName> -P <Password File> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -l <UserName> -P <Password File> <IP> <telnet|ftp|ssh|rdp>
# hydra -V -f -L <UserName File> -p <Password> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -L <UserName File> -p <Password> <IP> <telnet|ftp|ssh|rdp>
# hydra -V -f -L <UserName File> -P <Password File> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -L <UserName File> -P <Password File> <IP> <telnet|ftp|ssh|rdp>
# hydra -V -f -t 3 -l <UserName> -p <Password> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -t 5 -l <UserName> -P <Password File> <IP> <telnet|ftp|ssh|rdp>
# hydra -V -f -t 3 -L <UserName File> -p <Password> <telnet|ftp|ssh|rdp>://<IP>
# hydra -V -f -t 5 -L <UserName File> -P <Password File> <IP> <telnet|ftp|ssh|rdp>
-l LOGIN or -L FILE  login with LOGIN name, or load several logins from FILE
-p PASS  or -P FILE  try password PASS, or load several passwords from FILE
-s PORT              if the service is on a different default port, define it here
-f / -F              exit when a login/pass pair is found (-M: -f per host, -F global)
-v / -V / -d         verbose mode / show login+pass for each attempt / debug mode
-t TASKS             run TASKS number of connects in parallel per target (default: 16)
-T TASKS             run TASKS connects in parallel overall (for -M, default: 64)
-w / -W TIME         wait time for a response (32) / between connects per thread (0)

# hydra -V -f -l <UserName> -x 1:1:aA1 192.168.0.1 rdp
-x MIN:MAX:CHARSET   password bruteforce generation, type "-x -h" to get help
 MIN     is the minimum number of characters in the password
 MAX     is the maximum number of characters in the password
 CHARSET is a specification of the characters to use in the generation
            valid CHARSET values are: 'a' for lowercase letters,
            'A' for uppercase letters, '1' for numbers, and for all others,
            just add their real representation.
 -y         disable the use of the above letters as placeholders
 Examples:
  -x 3:5:a       generate passwords from length 3 to 5 with all lowercase letters
  -x 5:8:A1      generate passwords from length 5 to 8 with uppercase and numbers
  -x 1:3:/       generate passwords from length 1 to 3 containing only slashes
  -x 5:5:/%,.-   generate passwords with length 5 which consists only of /%,.-
  -x 3:5:aA1 -y  generate passwords from length 3 to 5 with a, A and 1 only
```
---

##### [OWASP ZAP](https://www.zaproxy.org/)
###### [wiki](https://en.wikipedia.org/wiki/OWASP_ZAP)
###### [OWASP Testing Guide v4 Table of Contents](https://wiki.owasp.org/index.php/OWASP_Testing_Guide_v4_Table_of_Contents)
```
# owasp-zap
```
---

##### hping3(8) - send (almost) arbitrary TCP/IP packets to network hosts
```
# hping3 -q -n -a 10.0.0.1 --udp -s 53 --keep -p 68 --flood 192.168.0.1
# hping3 -i u10000 -S -p 80 192.168.0.1
# hping3 -c 10 -d 120 -S -w 64 -p 21 --flood --rand-source 192.168.0.1
-i  --interval (uX for X microseconds, for example -i u1000)
-c 10: Number of packets to send.
-d 120: Size of each packet that was sent to target machine.
-S: sending SYN packets only.
-w 64: TCP window size.
-p 21: Destination port (21 being FTP port).
--flood: Sending packets as fast as possible, without taking care to show incoming replies. Flood mode.
--rand-source: Using Random Source IP Addresses. You can also use -a or –spoof to hide hostnames.
```
---

##### [Hyenae](https://sourceforge.net/projects/hyenae/)
```
> hyenae.exe -I 5 -a tcp -f s -s %-%@%%%% -d 00:11:22:33:44:55-192.168.0.2@9 -e 1 -E 1000
```
---
