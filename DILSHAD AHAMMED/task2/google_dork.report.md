# Google Dorking Report: Publicly Exposed Documents or Directories from

**ferrari.com**

---

### **Objective**

Use Google Dorks to identify publicly accessible files or directories on `ferrari.com` that may contain potentially sensitive or interesting information. All information was discovered using legal, ethical, and public search engine techniques.

---

### **Entry 1: Confidential PDF Document**

* **Google Dork Used:**
  `site:ferrari.com filetype:pdf "confidential"`

* **Link to Exposed File:**
  [https://www.ferrari.com/content/dam/ferrari-fcom/old/pdf/CS\_296\_Speciale\_A\_gbr.pdf](https://www.ferrari.com/content/dam/ferrari-fcom/old/pdf/CS_296_Speciale_A_gbr.pdf)

* **File Type:** PDF

* **Title:** Ferrari 296 Speciale A (Product Sheet)

* **Description:**
  The PDF is marked multiple times with `Confidential - Internal Use Only`. Although publicly accessible, the document contains internal designations suggesting it was intended for restricted audiences. It includes branding materials and marketing assets that are not intended for general public distribution.

---

### **Entry 2: Admin Path Discovered (Redirects to Zendesk)**

* **Google Dork Used:**
  `site:ferrari.com inurl:admin "admin"`

* **Link Found:**
  [https://support.store.ferrari.com/hc/admin/general\_settings?locale=ja](https://support.store.ferrari.com/hc/admin/general_settings?locale=ja)

* **Redirects to:**
  [https://thelevelgroup.zendesk.com/auth/v2/login/signin?...](https://thelevelgroup.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Fsupport.store.ferrari.com%2Fhc%2Fadmin%2Fgeneral_settings%3Flocale%3Dja&theme=hc&locale=en-us&brand_id=10505614015644&auth_origin=10505614015644%2Ctrue%2Ctrue&role=agent)

* **File Type:** Web Page / Admin Interface (Zendesk)

* **Description:**
  This URL appears to point to a Ferrari support/admin backend but redirects to a Zendesk login page hosted by a third party vendor (The Level Group). Although authentication is required, discovering this path indicates internal helpdesk or administrative tooling integration that could be of interest in a penetration testing context.

---

## 📊 Summary Table

| # | Google Dork Used                               | Description                                  |
| - | ---------------------------------------------- | -------------------------------------------- |
| 1 | `site:ferrari.com filetype:pdf "confidential"` | Located internal-use-only PDF                |
| 2 | `site:ferrari.com inurl:admin "admin"`         | Found admin path, redirects to Zendesk login |

---

**Prepared By:** *DILSHAD AHAMMED N*

**Date:** July 19, 2025