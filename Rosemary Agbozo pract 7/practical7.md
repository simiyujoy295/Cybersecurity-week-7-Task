# PART 1: port scanning using nmap 

1. 1 ICMP ping
sudo nmap -sP -PE 10.0.2.15/24 

Output: 4 hosts up - full result in screenshot


1. 2 TCP ping
nmap -p 389 10.0.2.15/24 <!--pinging port number 389 tcp -->

Output: port 389/tcp was closed for the host 10.0.2.15. other hosts were filtered.

1. 3 TCP connect scan
nmap -sT 10.0.2.15
 <!--Or for the whole network-->
nmap -sT 10.0.2.0/24

Output: Port 22/tcp was open (service - ssh)



1. 4 Stealth scanning
sudo nmap -sS 10.0.2.15 <!--requires root privileges-->

1. 5 UDP scanning
sudo nmap -sU 10.0.2.15 <!--perfomed for a particular host, can be performed for the network using 10.0.2.0/24 network address-->

1. 6 stealth fin
sudo nmap -sF 10.0.2.15 

1. 7 vulnerabilities using vuln --script 
sudo nmap -v --script vuln 192.168.56.1

#Some vulnerabilites were the: 
1. Slowloris DOS attack on ports 80, 135, 139, 443, etc.
This is a denial of service attack. It uses partial HTTP requests to establish a connection between a single computer and the targeted server. It keeps these connections open, thus overwhelming the server, and rendering the server inaccessible to further requests bt the client. In other words, slowloris tries to keep many connections to the target web server open and hold them open as long as possible. It accomplishes this by opening connections to the target web server and sending a partial request. Periodically, it will send subsequent HTTP headers, adding to-but never completing-the request. Affected servers will keep these connections open, filling their maximum concurrent connection pool, eventually denying additional connection attempts from clients.
2. Diffie-Hellman Key Exchange Insufficient Group Strength.
This vulnerability allows for the logjam attack against the TLS protocol. The Logjam attack allows a man-in-the-middle attacker to downgrade vulnerable TLS connections to 512-bit export-grade cryptography. This allows the attacker to read and modify any data passed over the connection.  







#PART 2: Cracking a hash-->

2. 1 I used hash-identifier to first find the Hash used, which was SHA-1  -->
hash-identifier <!-- when it run, i pasted the hash string in it-->

2. 2 I tried hashcat and johntheripper in Kali, the hash was not in the word list, so I used an SHA1 decoder site. 
#The password is:  jrahyn+ 

<!-- Screenshot of result in folder-->


#PART 3

#Public key encryption with openssl

 3. 1  Fisrt, create a small file that we will later encrypt, and type something inside
 nano file1.txt 

 3. 2  Generate the private rsa key and save it into a pem file
 openssl genrsa -out privatekey.pem 2048

3. 3  Generate/extact and save the corresponding public key into another pem file
openssl rsa -in privatekey.pem -pubout -out publickey.pem

3. 4 Encrypt the file1.txt with public key and store it in a new file called encfile1.txt
openssl rsautl -encrypt -in file1.txt -out encfile1.txt -inkey publickey.pem -pubin 

3. 5 Decrypt the file "encfile1.txt" using the private key and store the decrypted text in decfile1.txt
openssl rsautl -decrypt -in encfile1.txt -out decfile1.txt -inkey privatekey.pem

3. 6 Cat into decfile1.txt to compare with original file
cat decfile1.txt

#Output matches originl







