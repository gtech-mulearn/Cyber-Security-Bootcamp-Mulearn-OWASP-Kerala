# Discovering Sensitive Files Through Google Dorking: A Practical Insight

While exploring publicly available resources through Google Search, I analyzed the **robots.txt** file hosted under the Amazon Flex domain using the query:

site:flex.amazon.com filetype:txt

This Google Dork reveals publicly accessible `.txt` files hosted on the Amazon Flex domain. Among the files discovered were:

- **robots.txt** – instructs web crawlers what to index  
- **security.txt** – provides security contact information for reporting vulnerabilities (if present)  

---

## 📸 Screenshot

Here is an example screenshot from the reconnaissance process:

![Google Dorking Screenshot](screenshot.png)

---

## 1. robots.txt – Indexing Instructions

The `robots.txt` file is found at the root of most websites (e.g., https://flex.amazon.com/robots.txt). It provides indexing rules for search engine crawlers.

### ✅ Allowed Resources
The file may explicitly allow indexing of public-facing resources such as:
- CSS and JavaScript files (e.g., `/assets/*.css`, `/scripts/*.js`)
- Images (`*.jpg`, `*.png`)
- Select public directories (`/help/`, `/static/`)

These allowances help search engines render the website properly in search results.

### 🚫 Disallowed Resources
More importantly, the file often disallows access to sensitive internal paths, including:

- System directories like `/admin/`, `/internal/`, `/config/`
- Setup or log files such as:
  - `/INSTALL.txt`
  - `/CHANGELOG.txt`
  - `/cron.php`

> ⚠️ **Note:** Disallowing files in `robots.txt` prevents indexing by well-behaved search engines — it does not restrict direct access if the URL is known.

---

## 2. security.txt – Responsible Disclosure Policy

If a `security.txt` file exists, it is typically located at:

https://flex.amazon.com/.well-known/security.txt

This file provides a clear channel for ethical hackers to report vulnerabilities. Typical contents include:

- **Contact:** Email or URL to report issues  
- **Encryption:** PGP key for secure communication  
- **Acknowledgments:** How researchers are credited  
- **Policy:** Link to vulnerability disclosure or bug bounty policy  
- **Expires:** Expiration date of the policy  

> Not all domains implement `security.txt`, but it’s a modern best practice for transparency.

---

## 🔐 Security Reflection

Files like `robots.txt` and `security.txt` are intended for transparency and indexing guidance, yet they can reveal information useful during reconnaissance:

- `robots.txt` can unintentionally expose internal structure  
- `security.txt` helps build trust and a responsible reporting pathway  

Both should not substitute proper security mechanisms such as access control, input validation, or encryption.

---

## ✅ Best Practices for Web Security

- Never rely on `robots.txt` for security — treat it as advisory only  
- Protect sensitive directories with authentication  
- Regularly audit public files and directories  
- Monitor indexing using Google Search Console  
- Keep `security.txt` updated with valid contact/encryption details  
- Ensure all communications use **HTTPS**  

---

## 🏁 Conclusion

By analyzing Amazon Flex’s publicly visible files, we gain insights into how web structure and disclosure files interact with search engines and ethical hacking. Proper management ensures transparency without compromising real security.

