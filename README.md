# Cybersecurity-week-7-Task

This weeks Practical Activity has 3 parts which are quite important in the Reconnaissance stage of Penetration Testing.   

Part 1: based on port scanning using Nmap 

Part 2: Cracking a Hash using whatever tool you are comfortable with. 

Part 3: Encryption with OpenSSL  

 

## Submission Procedure. 

1. All the commands used should be well documented using Markdown format. Eg. Practicalactivity.md 

2. Then separately attach all screenshots you have taken for every procedure/command. – The format for naming screenshot in every step is eg.Part1_1.png, Part2_1.png, Part3_1.png make sure the screenshot is identified by Part 1,2,3 to know the question you are answering. 

3. The save all your work in a single folder with your name  

4. The push your work to this GitHub repo using the procedure given. 

 

## Part 1: Perform the following scans on your Kali linux machine and attach the code and output of each command. 

Icmp ping                      

tcp ping                         

TCP connect                 

Stealth Scanning            

UDP Scanning              

Stealth FIN    

Find any Vulnerabilities within your host network using vuln --script and state how you can exploit them                

## Part 2: Cracking a Hash using whatever tool you are comfortable with and screenshot the answer.  

A hacker leaked the below hash online. Can you crack it to know the password of the CEO? the flag is the password Hash: 06f8aa28b9237866e3e289f18ade19e1736d809d 

 

 

 

## Part 3: Public key encryption with OpenSSL 

What to turn in: A listing of the exact commands you used to accomplish the tasks below. 

It is up to you to figure out the exact commands. This time we are using public key cryptography. This is only designed to operate on a small amount of data, so run it on a very small file. 

Complete the following tasks: 

1. Generate a RSA private key and save it to a file. The command you should be using is openssl genrsa 

2. Generate and save a corresponding RSA public key. The command needed here is openssl rsa 

3. Encrypt a file using your RSA public key. The command needed is openssl rsautl 

4. Decrypt the file using your RSA private key. Verify that the output matches the original. 
