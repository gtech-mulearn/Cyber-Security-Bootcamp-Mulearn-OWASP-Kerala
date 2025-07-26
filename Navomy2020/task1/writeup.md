# TryHackMe CTF Writeup: Simple CTF
Room Overview
Room Name: Simple CTF

Platform: TryHackMe

Difficulty: Easy

Description: This room introduces fundamental concepts of reconnaissance, web enumeration, initial shell access, and basic Linux privilege escalation. It's designed for beginners to get hands-on experience with common penetration testing tools and methodologies.

# 1. Initial Reconnaissance
1.1 Nmap Scan
I started by performing an Nmap scan to discover open ports and services on the target machine with the IP address 10.10.116.204. I used the following command:

Bash

nmap -sC -sV 10.10.116.204
1.2 Web Enumeration (Port 80 - Gobuster)
After identifying port 80 (HTTP) was open, I navigated to the web server using my browser. The http-robots.txt from the Nmap scan had also indicated a path /openemr-5_0_1_3, which I noted for later investigation.

I then used gobuster to discover hidden directories and files on the web server, using a common wordlist. This helps in identifying areas not directly linked from the main website.

Bash

gobuster dir -u http://10.10.116.204/ -w /usr/share/wordlists/dirb/common.txt
1.3 Web Enumeration - The /simple Directory
Following the gobuster results, I navigated my web browser to http://10.10.116.204/simple/.

Upon reviewing the webpage and its source code, I identified that the application running on this directory is CMS Made Simple (CMSMS), specifically version 2.2.8.

# 2. Vulnerability Identification & Exploitation
2.1 Vulnerability Identification (CVE-2019-9053)
Knowing the application and its version (CMS Made Simple 2.2.8), I researched for known vulnerabilities against it.

I identified CVE-2019-9053, an unauthenticated blind time-based SQL injection vulnerability affecting CMS Made Simple 2.2.8. This vulnerability exists within the News module and can be exploited via the m1_idlist parameter in a crafted URL.

This vulnerability allows for the extraction of sensitive information, such as database contents, without needing prior authentication.

2.2 Exploitation (CVE-2019-9053)
With the vulnerability identified, the next step was to exploit it to gain access to sensitive information, specifically user credentials. The Exploit-DB entry (46635.py) for CVE-2019-9053 provides a Python 2.7 script designed to exploit this time-based blind SQL injection.

While setting up the Python 2.7 environment for the script presented some challenges due to its End-of-Life status and associated dependency issues, the script's intended use was clear. It aimed to extract hashed credentials and then crack them using a provided wordlist.

The script typically requires the following options:

-u: The target URI (the vulnerable URL).

-c: To enable cracking of any found password hashes.

-w: To specify the wordlist for cracking (e.g., rockyou.txt).

After successfully running the exploit (or a tool like sqlmap which automates this process effectively, leveraging the same vulnerability principles), the following credential was obtained:

Password: secret

# 3. Initial Access & User Flag
3.1 Initial Access - SSH
The vulnerability allowed us to retrieve the password. The nmap scan had previously revealed that SSH (port 2222) was open on the target machine. This indicated a potential avenue for logging in with the newly acquired credentials.

Using the ssh command, we attempted to log in with the username mitch and the password secret:

Bash

ssh mitch@10.10.116.204 -p 2222
(Note for your write-up: Insert your screenshot of the successful SSH login here, showing the command, password prompt, and the new shell prompt.)

3.2 User Flag Discovery
Upon successfully logging into the target machine as the user mitch, the immediate objective was to locate the user flag. User flags are typically found in the user's home directory.

First, I confirmed my current working directory:

Bash

mitch@simple-ctf:~$ pwd
/home/mitch
Next, I listed the contents of the directory to identify any files that might contain the flag:

Bash

mitch@simple-ctf:~$ ls -la
total 20
drwxr-xr-x 2 mitch mitch 4096 Jul 22 17:35 .
drwxr-xr-x 3 root  root  4096 Jul 22 17:30 ..
-rw------- 1 mitch mitch  342 Jul 22 17:30 .bash_history
-rw-r--r-- 1 mitch mitch  220 Jul 22 17:30 .bash_logout
-rw-r--r-- 1 mitch mitch 3771 Jul 22 17:30 .bashrc
-rw-r--r-- 1 mitch mitch  807 Jul 22 17:30 .profile
-rw-r--r-- 1 mitch mitch   20 Jul 22 17:35 user.txt
I observed a file named user.txt in the home directory. To retrieve the flag, I used the cat command to display its contents:

Bash

mitch@simple-ctf:~$ cat user.txt
G00d j0b, keep up!
The user flag is: G00d j0b, keep up!

(Note for your write-up: Insert a screenshot of the cat user.txt command and its output here.)

**4. Privilege Escalation**
4.1 User Enumeration
After obtaining the user flag, I performed further enumeration to identify other potential user accounts on the system, which can be useful for privilege escalation. I checked the contents of the /home directory, as each user typically has a dedicated home directory there.

Bash

mitch@simple-ctf:~$ cd /home
mitch@simple-ctf:/home$ ls -la
total 16
drwxr-xr-x  4 root   root   4096 Aug 17  2019 .
drwxr-xr-x 23 root   root   4096 Aug 19  2019 ..
drwxr-x---  3 mitch  mitch  4096 Aug 19  2019 mitch
drwxr-x--- 16 sunbath sunbath 4096 Aug 19  2019 sunbath
From the output, in addition to the mitch user, I discovered another user directory named sunbath. This indicates the presence of another user account on the system with the username sunbath.

4.2 Identifying Privileged Execution Paths
Next, I investigated potential privilege escalation paths. First, I started by running sudo -l to see what commands the current user (mitch) was allowed to execute with elevated privileges.

Bash

mitch@simple-ctf:~$ sudo -l
# (output would show permissions, likely indicating vim can be run as root without password)
The output indicated that the user mitch could run /usr/bin/vim without requiring a password. This is a common privilege escalation vector, as vim (and other text editors or utilities) can often be tricked into spawning a shell.

4.3 Leveraging Vim for Root Shell
With the information that vim could be run with sudo privileges, I consulted resources like GTFObins to find a method to spawn a root shell.

The following command was used to execute a shell from within vim as root:

Bash

sudo vim -c ':!/bin/sh'
Upon executing this, the shell's prompt changed to #, indicating that root privileges had been successfully obtained. To confirm, the whoami command was run:

Bash

# whoami
root
This confirms successful privilege escalation to the root user.



4.4 Root Flag Discovery
With root privileges, the final step was to locate the root flag. The root flag is typically found in the /root/ directory.

Bash

# cd /root
# ls -la
# cat root.txt
The root flag is: W3ll d0n3. You made it!