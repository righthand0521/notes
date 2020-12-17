Command
===


##### A space before a bash command is not recorded in history
---

##### awk(1) - pattern scanning and processing language
```
awk 'pattern + {action}'
# awk '{print $0}'
# awk '{print $NF,$0}'
# awk '{print substr($0,2,length($0)-2)}'
# awk '{if(length($0)>20) print $0}'
# awk '/inet / {print $2}'
# awk '/inet addr/ {print substr($2,6)}'
# awk '{a[$2]++}END {for(i in a) {print a[i] " " i}}'
# awk '{total+=$2}END {print total}'
# awk 'match($0, /[[:digit:]]{10}([^,]+)/) { print substr( $0, RSTART, RLENGTH )}'

# awk -F":" '{print $1}'
# awk -v s=$start '$1 >= s && $1 <= $(date"+%s") {print}'

remove newline
# awk NF=NF RS= OFS=+
```
---

##### bc(1) - An arbitrary precision calculator language
```
# echo "5+50*3/20 + (19*2)/7" | bc
# echo "5+50*3/20 + (19*2)/7" | bc -l
# echo "scale=3; 5+50*3/20 + (19*2)/7" | bc -l
# printf "%.3f\n" $(echo "5+50*3/20 + (19*2)/7" | bc -l)
```
---

##### crontab(1) - maintain crontab files for individual users (Vixie Cron)
```
# ls -l /var/spool/cron/crontabs/
```
```
# m h  dom mon dow   command
# m分鐘(0-59), h小時(0-23), dom日期(1-31), mon月份(1-12), dow星期(0-6), command需要執行的command.
# '*'    代表任何時刻都接受的意思
# ','    代表分隔時段        30 9,17 * * * command => 早上9點半和下午五點半都執行command
# '-'    代表一段時間範圍    15 9-12 * * * command => 從9點到12點的每個15分都執行command
# '/n'   代表每n個單位間隔   */5 * * * *   command => 每隔5分鐘執行一次command)
#
# For more information see the manual pages of crontab(5) and cron(8)
# @reboot  Run once at startup
# @yearly  Run once a year     0 0 1 1 * command
# @monthly Run once a month    0 0 1 * * command
# @weekly  Run once a week     0 0 * * 0 command
# @daily   Run once a day      0 0 * * * command
# @hourly  Run once an hour    0 * * * * command
```
```
0 1 * * *           tar -zcvf $(date +"\%Y\%m\%d").tgz /var/lib/jenkins/jobs
0 0,6,12,18 * * *   tar -zcvf /root/`date +"\%Y\%m\%d"`.tgz tmp/; chmod 744 `date +"\%Y\%m\%d"`.tgz
```
---

##### curl(1) - transfer a URL
```
# curl ipinfo.io
# curl ifconfig.me
# curl v4.ifconfig.co
# curl v6.ifconfig.co
```
```
# curl --connect-timeout 3 --max-time 3 --retry 3 <HTTP URL>
# curl --local-port $(((RANDOM%10000)+10000)) <HTTP URL>
# curl -w "Status Code: %{http_code}" <HTTP URL>
# curl <HTTP URL> --output <Local File Path>
# curl -s --insecure <HTTP URL>
```
```
# curl -v --proxy-insecure -x https://192.168.0.1:3128 -k -L https://www.google.com/
# curl -v --proxy-insecure -x https://admin:password@192.168.0.1:3128 -k -L https://www.google.com/
```
```
通過使用 -v 和 -trace獲取更多的連結資訊

列出public_html下的所有資料夾和檔案
# curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/
下載xss.php檔案
# curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/xss.php

上傳檔案到FTP伺服器, 通過 -T 選項可將指定的本地檔案上傳到FTP伺服器上
將myfile.txt檔案上傳到伺服器
# curl -u ftpuser:ftppass -T myfile.txt ftp://ftp.testserver.com
同時上傳多個檔案
# curl -u ftpuser:ftppass -T "{file1,file2}" ftp://ftp.testserver.com
從標準輸入獲取內容儲存到伺服器指定的檔案中
# curl -u ftpuser:ftppass -T - ftp://ftp.testserver.com/myfile_1.txt
```
---

##### cut(1) - remove sections from each line of files
```
This prints each line of the input starting at column 6
# cut -c6- <file>
```
---

##### date(1) - print or set the system date and time
```
# date +"%Y/%m/%d %H:%M:%S"
# date +"%Y/%m/%d %H:%M:%S" -d yesterday
# date +"%Y/%m/%d %H:%M:%S" --date='@2147483647'
# date -D "%s" -d $(( $(date +%s) - 86400))
# date -s @'1558403074'

Date to Timestamp
# date -d "2019-10-06T22:20:36+08:00" +%s

Timestamp to Date
# date "+%Y-%m-%d %T" --date=@1601867260

# while sleep 1; do tput sc; tput cup 0 $(($(tput cols)-32)); date +"%s: %Y/%m/%d %H:%M:%S"; tput rc; done
```
---

##### dd(1) - convert and copy a file
```
# dd if=/dev/zero of=zero.dat; rm -f zero.dat
# dd if=/dev/zero of=1MB count=1024 bs=1024
```
---

##### diff(1) - compare files line by line
```
# diff -ruN ori/ new/ > file.patch
-r: recursive, so do subdirectories.
-u: unified style, if your system lacks it or if recipient may not have it, use "-c".
-N: treat absent files as empty.
```
---

##### dos2unix(1) - DOS/MAC to UNIX text file format converter
```
# apt install dos2unix

# find . -type f -print0 | xargs -0 dos2unix
```
---

##### dpkg(1) - package manager for Debian
```
列出已安裝的'package'
# dpkg -l
顯示該'package'的版本
# dpkg -l package
列出與該'package'關聯的文件
# dpkg -L package
```
---

##### du(1) - estimate file space usage
```
# du --max-depth=1 -h <path>
```
---

##### find(1) - search for files in a directory hierarchy
```
# find . -name "*.asp" -exec bash -c 'mv "$1" "${1%.asp}".html' - '{}' \;

# find . -name "*.o" -exec ls -l {} \;
# find . -regex '.*\(so\|pyc\|xml\|html\)$' -exec ls -l {} \;
# find . -type f -newermt 2018-12-01 ! -newermt 2018-12-02 -exec ls -l {} \;

# find . -name "*.o" -exec echo rm -rf {} \; -exec rm -rf {} \;
# find . -regex '.*\(so\|pyc\|xml\|html\)$' -exec echo rm -rf {} \; -exec rm -rf {} \;
# find . -type f -newermt 2018-12-01 ! -newermt 2018-12-02 -exec echo rm -rf {} \; -exec rm -rf {} \;

https://stackoverflow.com/questions/2709458/how-to-replace-spaces-in-file-names-using-a-bash-script
# find -name "* *" -type d | rename 's/ /_/g'
# find -name "* *" -type f | rename 's/ /_/g'
```
---

##### ftpput(1) - Upload a file to a ftp server
```
ftpput -u <ID> -p <PW> -P <Port> <IP Address> <dst target path> <src file path>
```
---

##### grep(1) - print lines matching a pattern
```
# grep -rl ".asp" . | xargs -i sed -i 's/.asp/.html/g' {}
```
---

##### history(3) - GNU History Library
```
List of commands you use most often
# history | awk '{a[$2]++}END {for(i in a) {print a[i] " " i}}' | sort -rn | head
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

##### httperf(1) - HTTP performance measurement tool
```
# httperf --hog --server 192.168.0.1 --num-conn 2500 --rate 500 --num-call 1 --timeout 5 --port 80
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

##### ifconfig(8) - configure a network interface
```
# ifconfig eth0 | awk '/inet / {print $2}' | cut -f 2 -d :
# ifconfig eth0 promisc
# ifconfig eth0 -promisc
```
---

##### ip(8) - show / manipulate routing, devices, policy routing and tunnels
```
# ip addr show eth0 | awk '/inet / {print $2}' | cut -f 1 -d /

ip addr add [IP Address]/16 dev [Interface]
ip addr del [IP Address]/16 dev [Interface]

# ip link set eth0 mtu 1500
# ip link set eth0 promisc on
# ip link set eth0 promisc off

# ip route add 10.24.0.0/16 dev eth0
# ip route add 10.24.0.0/16 via 192.168.0.1 dev eth0
```
---

##### iperf(1) - perform network throughput tests
```
# iperf -s
# iperf -c 192.168.0.1 -w 100M -t 120 -i 10
-c 192.168.0.1: Server端的IP
-w 100M: 測試的檔案大小
-t 120: 監視測量數據時間為120秒
-i 10: 每隔10秒將數據顯示出來
```
---

##### iptables/ip6tables(8) — administration tool for IPv4/IPv6 packet filtering and NAT
```
# lsmod | grep ip_tables

# iptables -t filter -S; iptables -t nat -S; iptables -t mangle -S
# iptables -t filter -F; iptables -t nat -F; iptables -t mangle -F
# iptables -t filter -nL -v --line-number; iptables -t nat -nL -v --line-number; iptables -t mangle -nL -v --line-number

# iptables-save > /etc/iptables_rules
# /sbin/iptables-restore < /etc/iptables_rules
```
```
Port Forwarding
# sysctl -n net.ipv4.ip_forward
# sysctl net.ipv4.ip_forward=1
# vim /etc/sysctl.conf

# iptables -t mangle -A PREROUTING -d 10.24.13.253 -p tcp --dport 7722 -j MARK --set-mark 1 -i ens32
# iptables -t nat -A PREROUTING -p tcp -m mark --mark 1 -j DNAT --to-destination 192.168.127.33:7722 -i ens32
# iptables -t nat -A POSTROUTING -m mark --mark 1 -j SNAT --to-source 192.168.127.253 -o ens33
# iptables -A FORWARD -m mark --mark 1 -j ACCEPT -o ens33
```
---

##### jq(1) - Command-line JSON processor
```
jq 'todate'
# echo 0 | jq 'todate'
# echo 2147483647 | jq 'todate'
# echo 4294967297 | jq 'todate'
# jq -n '0 | strftime("%FT%T%z")'

# echo '{"a":"1", "b":"2", "c":"3"}' | jq -r 'keys[]'
# echo '[{"username":"user1"},{"username":"user2"}]' | jq '. | length'
# echo '{"users":[{"username":"user1"},{"username":"user2"}]}' | jq '.users | length'
# echo '[{"id":"u1", "pw":"p1"},{"id":"u2", "pw":"p2"}]' | jq -c '.[]'
# echo '[{"id":"u1", "pw":"p1"},{"id":"u2", "pw":"p2"}]' | jq -r '.[] | select(.id == "u2")'
# echo '[{"username":"user1"},{"username":"user2"}]' | jq '.+ [{"username":"user3"}]'
# echo '[{"id":"u1", "pw":"p1", "name":"n1"},{"id":"u2", "pw":"p2", "name":"n2"}]' | jq -r '. | keys[] as $k | "\($k), \(.[$k] | .id), \(.[$k] | .name)"'

--argjson
# echo ${rules} | jq --arg origIp ${origIp} --arg mapIp ${mapIp} '.[].name = $origIp | .[].origIp = $origIp | .[].mapIp = $mapIp | del(.[].cidr)'

Update one value in array of dicts, using jq
# echo '[{"format":"geojson","id":"foo"},{"format":"geojson","id":"bar"},{"format":"zip","id":"baz"}]' | jq 'map(if .id=="baz" then .format="csv" else . end)' | jq -c .
# echo '[{"format":"geojson","id":"foo"},{"format":"geojson","id":"bar"},{"format":"zip","id":"baz"}]' | jq 'map((select(.id == "baz") | .format) |= "csv")' | jq -c .
```
---

##### ln(1) - make links between files
```
ln -s <target path><symbolic path>
```
---

##### man(1) - an interface to the on-line reference manuals
```
Convert man Page Info to pdf Format: man -t <Command Name> | ps2pdf - <File Name>.pdf
# man -t ls | ps2pdf - ls.pdf
```
---

##### netstat(8) - Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships
```
# netstat -ntulp
t: tcp
u: udp
n: don't resolve names
l: display listening server sockets
p: display PID/Program name for sockets
```
---

##### nl(1) - number lines of files
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

##### openssl(1) - OpenSSL command line tool
```
# apt install libpcap-dev libssl-dev -y

# openssl version -a
# openssl ciphers -v
```
```
Generate ROOT CA
# openssl genrsa -des3 -out CA.key 2048
# chmod og-rwx CA.key
# openssl req -new -key CA.key -out CA.req
# openssl x509 -req -days 3650 -sha1 -extensions v3_ca -signkey CA.key -in CA.req -out CA.crt
# rm -f CA.req

Generate Server CA
# openssl genrsa -out FTPServer.key 1024
# chmod og-rwx FTPServer.key
# openssl req -new -key FTPServer.key -out FTPServer.req
# openssl x509 -req -days 730 -sha1 -extensions v3_req -CA CA.crt -CAkey CA.key  -CAserial CA.srl -CAcreateserial -in FTPServer.req -out FTPServer.crt
# rm -f FTPServer.req

Generate Client CA
# openssl genrsa -des3 -out ClientCA.key 2048
# chmod og-rwx ClientCA.key
# openssl req -new -key ClientCA.key -out ClientCA.req
# openssl x509 -req -days 730 -sha1 -extensions v3_req -CA RootCA.crt -CAkey RootCA.key  -CAserial RootCA.srl -CAcreateserial -in ClientCA.req -out ClientCA.crt
# rm -f ClientCA.req
# openssl pkcs12 -export -in ClientCA.crt -inkey ClientCA.key -out ClientCA.pfx
```
```
To encrypt with aes-256-cbc cipher
# openssl enc -aes-256-cbc -e -in <input_file> -out <output_file>

To decrypt an encrypted file
# openssl enc -aes-256-cbc -d -in <input_file> -out <output_file>

To list all available cipher algorithms
# openssl list-cipher-algorithms
```
---

##### patch(1) - apply a diff file to an original
```
# patch -p0 < file.patch
```
---

##### pcapfix(1) - repair pcap and pcapng files
```
# apt install pcapfix -y
```
---

##### ping, ping6(8) - send ICMP ECHO_REQUEST to network hosts
```
-q quiet
-c nb of pings to perform
```
---

##### pkill(1) - look up or signal processes based on name and other attributes
```
# pkill -kill -t pts/1
```
---

##### printenv(1) - print all or part of environment
```
# printenv PATH
# echo $PATH
```
---

##### pstree(1) - display a tree of processes
---

##### route(8) - show / manipulate the IP routing table
```
route [-A inet|inet6][-6] -n
route add default gw <IP Address> <Adapter>
route delete default gw <IP Address> <Adapter>
# route add -net 10.24.0.0/16 gw 192.168.0.1 eth0
```
---

##### rsync(1) - a fast, versatile, remote (and local) file-copying tool
```
rsync -azP <source> <destination>
```
---

##### scp(1) — secure copy (remote file copy program)
```
scp <Local Path> <Remote User>@<Remote IP>:/<Remote Path>
scp <Remote User>@<Remote IP>:/<Remote Path> <Local Path>
```
---

##### sed(1) - stream editor for filtering and transforming text
```
Remove NewLine
# sed ':a;N;$!ba;s/\n/+/g'

# sed ':a;N;$!ba;s/\n/\n\t\t/g'
# sed -r "s/\x1B\[([0-9]{1,2}(;[0-9]{1,2})?)?[mGK]//g"
# sed 's/^M$//'
# sed 's/\r$//'

# sed -i 's#\(.*/root:\).*#\1/bin/sh#' /etc/passwd

# ori_content='KERN_DIR="/usr/src/linux-headers-'$version'"'
# mdy_content='KERN_DIR="/usr/src/linux-headers-3.19.0-25-generic"'
# sed -i -e "s#$ori_content#$mdy_content#" test.config

# echo "10.24.0.1" | sed -e 's/10.24.0/192.168.1/g'
# t1="10.24.0"; t2="192.168.1"; echo "10.24.0.1" | sed -e "s/$t1/$t2/g"

Removing ANSI Color Codes from Text Stream
# echo -e '\e[0;32m{"ip":"192.168.0.1","online":true}\e[0m' | sed 's/\x1b\[[0-9;]*m//g'
# echo -e '\e[0;32m{"ip":"192.168.0.1","online":true}\e[0m' | sed -r "s/\x1B\[([0-9]{1,3}(;[0-9]{1,2})?)?[mGK]//g"
```
---

##### seq(1) - print a sequence of numbers
```
# seq -w 1 11
```
---

##### ser2net(8) - Serial to network proxy
```
# apt install ser2net -y
# cat /etc/ser2net.conf
# service --status-all
# update-rc.d ser2net enable
# systemctl enable ser2net
```
---

##### socat(1) - Multipurpose relay (SOcket CAT)
```
# apt install socat -y
```
---

##### ssh(1) - OpenSSH SSH client (remote login program)
```
ssh -o ConnectTimeout=10 -o StrictHostKeyChecking=no root@<IP>

ssh -vv -oCiphers=aes128-cbc,3des-cbc,blowfish-cbc <IP>
ssh -vv -oMACs=hmac-md5 <IP>

ssh -o "Compression yes" -vv <IP>
ssh -o "Compression no" -vv <IP>

ssh -C -vv <IP>
```
---

##### sshpass(1) - noninteractive ssh password provider
```
# apt install sshpass -y

Provide password as argument (security unwise)
# sshpass -p <password> ssh -o StrictHostKeyChecking=no -p <port> <username>@<IP> '<command>'

Take password to use from file
# sshpass -f <password filename> ssh -o StrictHostKeyChecking=no -p <port> <username>@<IP> '<command>'

Password is passed as env-var "SSHPASS"
# export SSHPASS='password'
# sshpass -e ssh -o StrictHostKeyChecking=no -p <port> <username>@<IP> '<command>'

Use number as file descriptor for getting password
# sshpass -d <number> ssh -o StrictHostKeyChecking=no -p <port> <username>@<IP> '<command>'
With no parameters - password will be taken from stdin

scp remote file to local
# sshpass -p <password> scp <username>@<IP>:$<remote path> <local path>

scp local file to remote
# sshpass -p <password> scp <local path> <username>@<IP>:$<remote path>
```
---

##### stat(1) - display file or file system status
```
stat -c "%a %n" <file path>
```
---

##### strace(1) - trace system calls and signals
```
strace -f <cmd>
# strace -f ping localhost &> log

strace -p <pid>
# strace -p $(ps aux | grep ping | grep -v grep | awk '{print $1}')
```
---

##### stty(1) - change and print terminal line settings
```
# stty -F /dev/ttyUSB0
speed 115200 baud; line = 0;
min = 1; time = 5;
ignbrk -brkint -icrnl ixoff -imaxbel
-opost -onlcr
-isig -icanon -iexten -echo -echoe -echok -echoctl -echoke

# stty -a -F /dev/ttyUSB0
# stty -F /dev/ttyUSB0 115200 -echo igncr -icanon onlcr ixon min 0 time 5
# stty -F /dev/ttyUSB0 speed 115200 cs8 -parenb -cstopb -echo
# exec 5<>/dev/ttyUSB0
# cat <&5
# echo "test" >&5
# exec 5<&-
```
---

##### tac(1) - concatenate and print files in reverse
---

##### tabs(1) - set tabs on a terminal
---

##### tail(1) - output the last part of files
```
tail -f <path> --pid=<pid>
```
---

##### tar(1) - an archiving utility
```
tar cvf <File>.tar <Dir Path>
tar xvf <File>.tar

tar zcvf <File>.tgz <Dir Path>
tar zxvf <File>.tgz

tar jcvf <File>.tbz2 <Dir Path>
tar jxvf <File>.tbz2
```
---

##### tcpdump(8) - dump traffic on a network
```
# tcpdump -C 100 -nnvvXSs 1514 -w `uname -n`_`date +"%Y%m%d%H%M%S"`.pcap
# tcpdump -G 86400 -nnvvXSs 1514 -w %Y%m%d%H%M%S.pcap

# tcpdump -r file.pcap
# tcpdump -xXr file.pcap | awk '{print $10}'

Split Pcap Size
# tcpdump -r <pcap file> -w <output pcap file> -C <Per Pcap Size>

# tcpdump -nn ether host aa:bb:cc:11:22:33
# tcpdump -nn src host 192.168.0.1
# tcpdump -nn not port 23
# tcpdump -nn udp and port 5353 and 5354
# tcpdump -nn net not 10.24.0.0/24

ARP
# tcpdump -nni eth0 arp
ICMP
# tcpdump -nni eth0 icmp
RIPv2
# tcpdump -i eth0 -v -s0 udp and port 520
RIPng
# tcpdump -i eth0 -v -s0 udp and port 521
DHCP
# tcpdump -i eth0 port 67 or port 68 -e -n
DHCPv6
# tcpdump -i eth0 port 546 or port 547 -e -n
LLDP
# tcpdump -i eth0 ether proto 0x88cc
```
---

##### telnet(1) - user interface to the TELNET protocol
```
# apt install telnet-ssl -y

# telnet fe80::d8ed:ef53:e0d3:336%eth0
# telnet -b <src ip> <dst ip>
```
---

##### timedatectl(1) - Control the system time and date
```
# timedatectl set-timezone 'Asia/Taipei'
# timedatectl set-timezone UTC
# timedatectl set-time "00:00:00"
```
---

##### timeout(1) - run a command with a time limit
```
# timeout --preserve-status -s 9 -k 3 3 ping 8.8.8.8
--kill-after=DURATION
--signal=SIGNAL
```
---

##### top(1) - display Linux processes
---

##### tr(1) - translate or delete characters
```
# tr -d '\015'
# tr -cd '\11\12\40-\176'
# tr -cd "[:print:]\t\r\n"
# tr -cd "[:print:]\f\v\t\r\n"
# tr -d "\n"

reverse a list of words
# echo "1 2 3 4 5" | tr ' ' '\n' | tac | tr '\n' ' '
```
---

##### ulimit(3) - get and set user limits
```
# ulimit -a
# kill -ABRT <pid>
# kill -SEGV <pid>
```
---

##### uniq(1) - report or omit repeated lines
---

##### upnpc(1) - miniupnpc library test client
```
# apt install miniupnpc

Add/Delete Port Mapping
# upnpc -a ip port external_port tcp | udp
# upnpc -d external_port tcp | udp

List Port Mapping and Status
# upnpc -l
# upnpc -s

External IP address
# upnpc -e

Initialize device list
# upnpc -i

Map these ports to this host
# upnpc -r port1 tcp | udp
```

###### [Use upnpc Mapping to External Network](http://blog.chinaunix.net/uid-20648944-id-3134810.html)
###### [Reference Manual: upnpc - interact with an external UPnP Internet Gateway Device](http://v2.nat32.com/upnpc.htm)
---

##### vmstat(8) - Report virtual memory statistics
---

##### wget(1) - The non-interactive network downloader
```
# wget -qO- v4.ifconfig.co
# wget -qO- v6.ifconfig.co
# wget -qO- icanhazip.com

# wget http://<IP> --http-user=<id> --http-password=<passwd>

# wget --spider -S http://192.168.0.1 | awk '/^  HTTP/{print $2}'
# wget --spider -S http://192.168.0.1 --http-user=root --http-password=password 2>&1 | awk '/^  HTTP/{print $2}'

# wget -e use_proxy=yes -e http_proxy=http://192.168.0.1:3128 http://askubuntu.com

# wget --user-agent="User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/42.0.2311.135 Safari/537.36 Edge/12.246" -qO- http://httpbin.org
# wget --user-agent="User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_1; en-US) AppleWebKit/532.0 (KHTML, like Gecko) Chrome/4.0.209.0 Safari/532.0" -qO- http://httpbin.org

# wget -r -np -R "index.html*" http://192.168.0.1/download/ -P /tmp -o /dev/null
```
---

##### xxd(1) - make a hexdump or do the reverse
---

##### yes(1) - output a string repeatedly until killed
```
https://codegolf.stackexchange.com/questions/21191/minimal-code-cpu-stress-tester
# yes :|sh&sleep 10;kill $!
# yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & sleep 10; killall yes

https://stackoverflow.com/questions/20200982/how-to-generate-a-memory-shortage-using-bash-script
# yes | tr \\n x | head -c $((20*1024*1024)) | grep n & sleep 1
```
---

##### zip(1) - package and compress (archive) files
```
# zip <FileName.zip> <DirName>
# unzip <FileName.zip>

# zip -e -r <FileName.zip> <DirName>
Enter password:
Verify password:
```
---
