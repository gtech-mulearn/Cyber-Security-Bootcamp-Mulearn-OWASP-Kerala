
# **Google Dorking Report – Tesla.com**

**Task 2: Public Reconnaissance Using Google Dorks**

---

## **Introduction**

This report is part of a cybersecurity assignment focused on using Google Dorks to identify publicly available resources on a target domain. The purpose is to demonstrate how search engines can sometimes index files or pages that were not meant to be accessed directly. The target for this task is **tesla.com**, the official website of Tesla Inc.

---

## **1. Find all PDF files**

**🔍 Dork Used:**

```
site:tesla.com filetype:pdf
```

**📌 What it does:**
Lists all PDF files hosted on tesla.com.

**✅ Examples Found:**

• Tesla Model S Owner’s Manual
[https://www.tesla.com/ownersmanual/models/pt\_pt/Owners\_Manual.pdf](https://www.tesla.com/ownersmanual/models/pt_pt/Owners_Manual.pdf)


• Tesla Model 3 Owner’s Manual
[https://www.tesla.com/ownersmanual/model3/sv\_us/Owners\_Manual.pdf](https://www.tesla.com/ownersmanual/model3/sv_us/Owners_Manual.pdf)

---

## **2. Find login pages**

**🔍 Dork Used:**

```
site:tesla.com inurl:login
```

**📌 What it does:**
Searches for URLs with the word “login”, which might point to admin or customer login pages.

**✅ Examples Found:**


• Feedback Login
[https://feedback.tesla.com/login](https://feedback.tesla.com/login)


• Solar Bonds Login
[https://solarbonds.tesla.com/a/login](https://solarbonds.tesla.com/a/login)

---

## **3. Search for PDFs containing the word “confidential”**

**🔍 Dork Used:**

```
site:tesla.com filetype:pdf intext:"confidential"
```

**📌 What it does:**
Looks for PDF documents that include the word “confidential” inside the text.

**✅ Example Found:**


• Tesla Investor Relations File
[https://ir.tesla.com/\_flysystem/s3/sec/000110465924059916/tm2413800d3\_defa14a-gen.pdf](https://ir.tesla.com/_flysystem/s3/sec/000110465924059916/tm2413800d3_defa14a-gen.pdf)

---

## **4. Look for text files**

**🔍 Dork Used:**

```
site:tesla.com filetype:txt
```

**📌 What it does:**
Shows text files such as configuration guides or robots.txt.

**✅ Example Found:**


• Robots.txt file
[https://www.tesla.com/robots.txt](https://www.tesla.com/robots.txt)

---

## **Conclusion**

Using simple Google Dorking techniques, I was able to identify a variety of public documents on tesla.com. These included user manuals, login pages, a potentially sensitive investor file, and standard configuration files. All the information was discovered using legal, passive reconnaissance methods via Google.

This task highlights how important it is for organizations to carefully manage what gets indexed by search engines—even when the content is technically public.

---
