# GoPhish Phishing

**Author:** Alvin Dennis
**Tool:** GoPhish (local instance)  
**Date:** 14/10/25
**Target group:** `test` (1 recipient)

---

## Objectives

- Verify end‑to‑end operation of GoPhish on a local host (`https://localhost:3333`).  
- Confirm ability to send campaign email via an SMTP sending profile.  
- Validate landing page functionality including capture of submitted form data and passwords.  
- Confirm reporting and status updates in GoPhish (Sent / Opened / Clicked / Submitted).

---

## Environment

- **GoPhish version:** _latest_  

- **Host:** Local machine — launched via:

```bash
./gophish
Accessed at `https://localhost:3333`. 
```

- **Admin controls:** Default admin password changed immediately after first login.  
- **SMTP:** Sending profile configured with `smtp.gmail.com:25` (Gmail account and credentials used for the profile).  
- **Landing page:** Cloned Google login form, with **Capture Submitted Data** and **Capture Passwords** enabled.  
- **Email template:** HTML template with personalization placeholders; previewed and tested in the editor.  
- **Target group:** Group `test` containing one user (first name, last name, email).  
- **Campaign:** Launched using the prepared template, landing page and sending profile; target = `test`.

---

## Methodology — step‑by‑step

1. **Install & start GoPhish:** Downloaded from the official repository and launched with `./gophish`.  
2. **Admin hardening:** Logged in at `https://localhost:3333` and changed the default admin password immediately.  
3. **Create sending profile:** `Sending Profiles → New Profile` — entered SMTP `smtp.gmail.com:25`, Gmail account and password, used **Send Test Email** to verify connectivity and add my sending profile for usage.  
4. **Landing page setup:** `Landing Pages → New Page` — cloned Google login form and enabled capture data and password. Saved page.  
5. **Create email template:** `Email Templates` — built HTML email with personalization placeholders; verified rendering.  
6. **Build target group:** `Users & Groups` — created `test` and added the single user.  
7. **Create & Launch campaign:** `Campaigns → New Campaign` — selected template, landing page, sending profile and `test` group; launched campaign.  
8. **Verify:** Confirmed dashboard updated to **Sent = 1**.

[Test Email](./assets/1.png)

[Landing Page](./assets/2.png)

[Group](./assets/3.png)

---

## Campaign results

- **Emails dispatched:** 1  

- **GoPhish dashboard status:** Sent = 1 (no additional events — Opened / Clicked / Submitted — were observed at the time of documentation.

---

## Conclusion

The test campaign demonstrated GoPhish is operational end‑to‑end for sending emails, rendering templates, serving landing pages, and capturing submitted outputs. The instance is suitable for further controlled and authorized testing, subject to the recommendations above to improve security, compliance, and operational procedures.