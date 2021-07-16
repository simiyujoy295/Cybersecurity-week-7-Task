PART 1(nmap scan)
1.	Icmp ping           nmap -sp 192.168.0.16               
2.    tcp ping            nmap -sP 192.168.0.16  
	    ┌──(root💀kali)-[/home/kali]
└─# nmap -sP 192.168.0.16
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 09:20 EDT
Nmap scan report for 192.168.0.16
Host is up (0.0012s latency).
Nmap done: 1 IP address (1 host up) scanned in 1.12 seconds
     
3.	TCP connect         nmap -sT 192.168.0.16
──(kali㉿kali)-[~]
└─$ nmap -sT 192.168.0.16
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 08:07 EDT
Nmap scan report for 192.168.0.16
Host is up (0.0049s latency).
Not shown: 993 filtered ports
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
902/tcp  open  iss-realsecure
912/tcp  open  apex-mesh
6881/tcp open  bittorrent-tracker

Nmap done: 1 IP address (1 host up) scanned in 16.89 seconds
   
4.	Stealth Scanning   nmap -sS 192.168.0.16 
	   ┌──(kali㉿kali)-[~]
└─$ sudo -s                                                                                                                               1 ⨯
[sudo] password for kali: 
┌──(root💀kali)-[/home/kali]
└─# nmap -sS 192.168.0.16            
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 08:08 EDT
Nmap scan report for 192.168.0.16
Host is up (0.0058s latency).
Not shown: 993 filtered ports
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
443/tcp  open  https
445/tcp  open  microsoft-ds
902/tcp  open  iss-realsecure
912/tcp  open  apex-mesh
6881/tcp open  bittorrent-tracker

Nmap done: 1 IP address (1 host up) scanned in 4.42 seconds

5.	UDP Scanning       nmap -sU 192.168.0.16  
	 ┌──(root💀kali)-[/home/kali]
└─# nmap -sU 192.168.0.16 
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 09:04 EDT
Nmap scan report for 192.168.0.16
Host is up (0.087s latency).
Not shown: 999 open|filtered ports
PORT     STATE  SERVICE
4500/udp closed nat-t-ike

Nmap done: 1 IP address (1 host up) scanned in 158.57 seconds

6.	Stealth FIN          nmap -sF 192.168.0.16 
	┌──(root💀kali)-[/home/kali]
└─# nmap -sF 192.168.0.16
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 09:11 EDT
Nmap scan report for 192.168.0.16
Host is up (0.0015s latency).
All 1000 scanned ports on 192.168.0.16 are open|filtered

Nmap done: 1 IP address (1 host up) scanned in 21.78 seconds
7.	Find any Vulnerabilities within your host network using vuln --script  
I decided to scan a vulnerable machine in my system instead of my network.The vulnerable machine is vulnerable to bruteforce. I decided to use a wildcard (*) to select scripts with a given name pattern. In this case i searched for vulnerabilities related to ftp and i found ftp-brute.         
──(kali㉿kali)-[~]
└─$ nmap --script "ftp-*" 192.168.255.128
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-16 09:52 EDT
NSE: [ftp-bounce] PORT response: 500 Illegal PORT command.
Stats: 0:06:59 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 25.00% done; ETC: 10:20 (0:20:54 remaining)
Stats: 0:06:59 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 25.00% done; ETC: 10:20 (0:20:54 remaining)
NSE: [ftp-brute] usernames: Time limit 10m00s exceeded.
NSE: [ftp-brute] usernames: Time limit 10m00s exceeded.
NSE: [ftp-brute] passwords: Time limit 10m00s exceeded.
Nmap scan report for 192.168.255.128
Host is up (0.0019s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
21/tcp open  ftp
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0              88 Jun 13  2019 note.txt
| ftp-brute: 
|   Accounts: No valid accounts found
|_  Statistics: Performed 3626 guesses in 602 seconds, average tps: 5.9
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.255.130
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.2 - secure, fast, stable
|_End of status

Nmap done: 1 IP address (1 host up) scanned in 603.62 seconds





PART 2 (Cracking a Hash )
The hash below is of SHA1 type
Hash: 06f8aa28b9237866e3e289f18ade19e1736d809d  = jrahyn+
The following is a link to the website i used to crack the hash:                                            https://md5hashing.net/hash/sha1/06f8aa28b9237866e3e289f18ade19e1736d809d







PART 3 (Encryption with OpenSSL)
A. Generation of private key with openssl genrsa
──(kali㉿kali)-[~]
└─$ Openssl genrsa -out private-key.pem 3072

B. Generation of public key with openssl rsa
──(kali㉿kali)-[~]
└─$ openssl rsa -in private-key.pem -pubout -out public-key.pem

C. Encrypting a simple file with RSA public key
pumkin - is the text file
encrypted.txt - this is the encrypted pumkin file
decrypted - this the file created after decrption of encrypted.txt
┌──(kali㉿kali)-[~]
└─$ openssl rsautl -encrypt -pubin -inkey public-key.pem -in pumkin -out encrypted.txt
┌──(kali㉿kali)-[~]
└─$ cat encrypted.txt
�S��o��ي�ib���W�!
�E6l���G��� U�v
��ލ�h��▒D���!55$8(������7�&hz��E��B�l<�r��Z1k]
z5))���4
�{�^p���{��R���+���[J�)
�`���B�����4c@�I�����㡓���L�/▒l�▒�R'�
                                     ɶ'm��VklQ�Zʎ���<���������ٿm��@x��J����U�ґ&�▒;��o   �3Q�����%����W�▒Kn�������Ɵ�ޡmf�� �A_    ��-���=������E��L%������{ȹ���Y�ߗ�
��B�5�7��n�o���7:8��=LP�▒�                                                                                                                                              


D. Decrypting the file encrypted using the RSA private key
┌──(kali㉿kali)-[~]
└─$ openssl rsautl -decryt -inkey private-key.pem -in encrypted.txt -out decrypted
┌──(kali㉿kali)-[~]
└─$ cat decrypted    

ssh to scarecrow : 5Qn@$y  


scarecrow@Pumpkin:~$ 




Oops!!! I just forgot; keys to the garden are with LordPumpkin(ROOT user)! 
Reach out to goblin and share this "Y0n$M4sy3D1t" to secretly get keys from LordPumpkin.

scarecrow@Pumpkin:~$ 

found other two user
LordPumpkin who appears to be root user
goblin



