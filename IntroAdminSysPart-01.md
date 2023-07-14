<h1 style="text-align: center;">Introduction to System Administration</h1>

<h5 style="text-align: center;color: #ABABAB;">Bendjelloul Noureddine</h5>

<hr>











[toc]

<div style="page-break-after: always;"></div>

# Linux / Bash

## Directory Navigation and Listing Commands

| Command             | Description                                  |
| ------------------- | :------------------------------------------- |
| cd                  | change to home directory                     |
| pwd                 | prints the current working directory         |
| cd  <directory>     | change to directly to specific directory     |
| ls                  | list content of current directory            |
| alias               | create a shortcut to another command         |
| rm                  | removes or deletes a file or directory       |
| mv                  | moves or renames a file or directory         |
| cat   <filename>    | print  <filename>  to screen                 |
| ps                  | list processes with pid                      |
| kill <PID>          | Kills the process with ID of <PID>           |
| passwd              | change password of the current user          |
| df                  | report disk space usage by filesystem        |
| date                | display or set date and time                 |
| head  <filename>    | print first lines of a file head  <filename> |
| tail     <filename> | print last lines of a file tail  <filename>  |
| which               | shows the full path of **shell** commands    |



<div style="page-break-after: always;"></div>

## Examples

### List file Command

```bash
$ ls
anaconda3	AndroidStudioProjects	Desktop 	Documents	Library 	Music     Public	Templates	Workspaces
$ ls -a
.                       .config    .gnupg              .mozilla      .redhat          .thunderbird
..                      Desktop    .gphoto             Music         .rest-client     .tmux.conf.d
anaconda3               Dev        .gradle             .nerd-font.d  .ServiceHub      AndroidStudioProjects   
LibrePCB-Workspace  	Desktop    .steam              Workspaces    .dotfiles 
$ ls -l
drwxrwxr-x 28 user user  4096 Jun 11 21:14 anaconda3
drwxr-xr-x  2 user user  4096 Jul 14 20:46 Desktop
drwxrwxr-x  8 user user  4096 Jul 13 23:53 Dev
drwxr-xr-x  3 user user  4096 Jul 14 20:45 Documents
drwxrwxr-x  3 user user  4096 Jul  2 23:43 Library
drwxr-xr-x  3 user user  4096 Jun 23 12:37 Music
drwxr-xr-x  3 user user  4096 Jun 12 00:10 Pictures
drwxr-xr-x  2 user user  4096 Jun  5 01:19 Templates
drwxr-xr-x  2 user user  4096 Jun  5 01:19 Videos
drwxrwxr-x  2 user user  4096 Jul 14 10:54 Workspaces

```

### Create Directory

```bash
$ mkdir test-dir/
$ ls
test-dir/
$ mkdir -p test-dirs/sub-dir-01
$ ls test-dirs/
sub-dir-01
```

### Copy and Move Files ( Dirs )

```bash
$ # cp <source> <destination>
$ # mv <source> <destination>
$ ls 
file.txt
$ cp file.txt new-name.txt
$ ls 
file.txt	new-name.txt
$ mv file.txt NewFileName.txt
$ ls 
NewFileName.txt		new-name.txt
```

### Remove Files and Dirs

```bash
$ ls -l
drwxrwxr-x 2 user user 4096 Jul 14 20:57 directory
-rw-rw-r-- 1 user user    0 Jul 14 20:57 file.txt
$ rm file.txt
$ ls
drwxrwxr-x 2 user user 4096 Jul 14 20:57 directory
$ # the -r argument means "recursively" and is required for directories
$ rm -r directory/   
$ ls
.
```

### Aliases

```bash
$ alias # shows all the list of aliases defined
alias l='ls'
alias l1='ls -1'
alias la='ls -alh'
alias ll='ls -lth'
$ alias dev="cd /home/user/dev"
$ ls
Desktop		Documents	Dev		Public
$ ls Dev/
project-01/		project-02/
$ dev
$ ls 
project-01/		project-02/ 	
```

#### Creating Permanent Aliases

You can store aliases in your user's shell configuration profile file to maintain them across sessions. It could be:

```bash
$ nano ~/.bashrc
```

Add your aliases anywhere towards the file's end

```sh
# ....
alias dockerup="docker compose up"
alias ssh-res="sudo systemctl restart sshd"
alias mock="mkdir mock/"
```

To enable the aliases, use : 

```bash
$ source ~/.bashrc
```





<div style="page-break-after: always;"></div>

# Networking

## Basic Networking Theory

Network architecture refers to the way network devices and services are structured to serve the connectivity needs of client devices <sup>Cisco</sup>.

* Network devices typically include switches and routers.
* Types of services include DHCP and DNS.
* Client devices comprise end-user devices, servers, and
  smart things.

## IPV 4 vs IPV 6

IPv4 is a version 4 of IP. It is a current version and the most commonly used IP address. It is a 32-bit address written in four numbers separated by 'dot', i.e., periods. This address is unique for each device.

For example, **66.94.29.13**

IPv4 produces 4 billion addresses, and the developers think that these addresses are enough, but they were wrong. IPv6 is the next generation of IP addresses. The main difference between IPv4 and IPv6 is the address size of IP addresses. The IPv4 is a 32-bit address, whereas IPv6 is a 128-bit hexadecimal address. IPv6 provides a large address space, and it contains a simple header as compared to IPv4. <sup>Javapoint</sup>

For example : **2001:db8:0:85a3:0:0:ac1f:8001**

## TCP/IP Ports and Protocols

A port is a virtual point where network connections start and end. Ports are software-based and managed by a computer's operating system.Ports are standardized across all network-connected devices, with each port assigned a number. Most ports are reserved for certain protocols.

| **Protocol**                                     | **Port Number** | **Description**                                              |
| ------------------------------------------------ | --------------- | ------------------------------------------------------------ |
| File Transfer Protocol (FTP)                     | 20/21           | On the Internet and on private networks, FTP is one of the most popular file transfer protocols. With only a basic understanding of networking, anyone can set up an FTP server, which makes it simple to transfer files from one system to another. |
| Secure Shell (SSH)                               | 22              | The main tool for managing network devices safely at the command level is SSH. Usually, it is used as a safe substitute for Telnet, which does not provide secure connections. |
| Telnet                                           | 23              | Telnet is a network protocol used to virtually access a computer and to provide a two-way, collaborative and text-based communication channel between two machines. |
| Simple Mail Transfer Protocol (SMTP)             | 25              | SMTP is used for two primary functions, it is used to transfer mail (email) from source to destination between mail servers and it is used by end users to send email to a mail system. |
| Internet Message Access Protocol (IMAP)          | 143             | The second major protocol used to get mail from a server is IMAP version 3. IMAP offers a larger range of remote mailbox activities than POP, which can be advantageous to users. |
| Domain Name System (DNS)                         | 53              | The DNS is used widely on the public internet and on private networks to translate domain names into IP addresses, typically for network routing. DNS is hieratical with main root servers that contain databases that list the managers of high level Top Level Domains (TLD) (such as .com). |
| Hypertext Transfer Protocol (HTTP)               | 80              | On most networks, HTTP is one of the most widely used protocols. Any client that accesses files stored on these servers uses HTTP, which is the primary protocol used by web browsers. |
| Hypertext Transfer Protocol over SSL/TLS (HTTPS) | 443             | In addition to HTTP, HTTPS is used to offer the same services, but with a secure connection that is supplied by either SSL or TLS. |
| FTP over TLS/SSL                                 | 989/990         | FTP over TLS/SSL utilizes the FTP protocol, which is subsequently secured using either SSL or TLS, much as the previous two entries. |

<div style="page-break-after: always;"></div>

## Networking in Linux

To manage your network under a Linux operating system, install the following packages

```bash
# Debian / Ubuntu
$ sudo apt-get install -y net-tools dnsutils bridge-utils nmap 
# Centos / Fedora
$ sudo dnf install net-tools bind-utils nmap # or yum
```

### IP

This is the latest and updated version of ifconfig command.

```bash
$ ip addr # or ip a 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
42: eth0@if43: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
```

For a more compact version 

```bash
$ ip -br a
lo               UNKNOWN        127.0.0.1/8 
eth0@if43        UP             172.17.0.2/16 
```

### Ping

Linux ping is one of the most used network troubleshooting commands. It basically checks for the network connectivity between two nodes.

```bash
$ # ping <destination> 
$ ping google.fr
PING google.fr (142.250.179.131) 56(84) bytes of data.
64 bytes from ams17s10-in-f3.1e100.net (142.250.179.131): icmp_seq=1 ttl=116 time=11.0 ms
64 bytes from ams17s10-in-f3.1e100.net (142.250.179.131): icmp_seq=2 ttl=116 time=12.6 ms
64 bytes from ams17s10-in-f3.1e100.net (142.250.179.131): icmp_seq=3 ttl=116 time=12.3 ms
...
```

### Dig

The dig command in Linux is used to gather DNS information. It stands for Domain Information Groper, and it collects data about Domain Name Servers.

```bash
$ # dig <domainName> 
$ dig google.fr
; <<>> DiG 9.18.12-0ubuntu0.22.04.2-Ubuntu <<>> google.fr
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55003
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.fr.			IN	A

;; ANSWER SECTION:
google.fr.		147	IN	A	142.251.39.99

;; Query time: 20 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Fri Jul 14 23:40:17 CEST 2023
;; MSG SIZE  rcvd: 54
```

### Nslookup

nslookup is a command-line tool to discover the IP address or DNS record of a specific domain name.

```bash
$ # nslookup <domainName>
$ nslookup imtech.staging.wissal-group.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	imtech.staging.wissal-group.com
Address: 51.77.211.113
```

<div style="page-break-after: always;"></div>

### Nmap

Nmap is a network scanning tool, an open source Linux command-line tool used for network exploration, host discovery and security auditing.

```bash
$ nmap -sn 192.168.1.0/24

Starting Nmap 7.80 ( https://nmap.org ) at 2023-07-14 23:50 CEST
Nmap scan report for mymodem (192.168.1.1)
Host is up (0.0061s latency).
Nmap scan report for Redmi-Note-11 (192.168.1.5)
Host is up (0.039s latency).
Nmap scan report for T14 (192.168.1.6)
Host is up (0.00017s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 3.11 seconds
```

## SSH

The SSH protocol (also referred to as Secure Shell) is a method for secure remote login from one computer to another. It provides several alternative options for strong authentication, and it protects communications security and integrity with strong encryption. It is a secure alternative to the non-protected login protocols (such as telnet, rlogin) and insecure file transfer methods (such as FTP).

### Key concept

* Authentication by Key 

- * Using **Public** / **Private Key**

- Password

- - Using a user based authentication 

- Port Configuration

- - Default : **22**

- SSH Client 

- - Is the application that enable the user to connect to other instances

- SSH Server

- - Referred as sshd (**ssh daemon**), is a process that turns in the server and it’s the one who enable other instances to connect to your server

  - The configuration file is located in **/etc/ssh/sshd_config**

  - - All the default configuration can be changed (like the PermitRootLogin, Port …)
    - It require **SUDO permissions**.

  - 

### Example

```bash
$ ssh <user>@<destination>
$ ssh ubuntu@my-server.com
# Use this command to create your pair of private / public keys
$ ssh-keygen
# Use the "-p" argument to specify the port number if it has been modified in the destination config
$ ssh -p 2222 ubuntu@my-server.com 
# Use the "-v" argument get the verbose log of your connection
$ ssh -v ubunut@my-server.com
# Use this command to copy your identity to the destination Host
$ ssh-copy-id <user>@<destination>
```

To use or modify the default ssh daemon settings open in sudo mode the file **/etc/ssh/sshd_config**

```bash
...
Port 2222 # the default was : 22
#ListenAddress 0.0.0.0
...
PermitRootLogin yes # the default was : prohibit-password
...
#PubkeyAuthentication yes
...
PasswordAuthentication no # the default was yes
#PermitEmptyPasswords no
...
```

