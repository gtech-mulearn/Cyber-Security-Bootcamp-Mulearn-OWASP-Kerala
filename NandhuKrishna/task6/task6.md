# GoPhish Simulated Phishing Campaign Report 🎣

[cite_start]**Prepared for:** Educational Purposes (e.g., MuLearn Bootcamp) [cite: 3]
[cite_start]**Date:** September 2025 [cite: 52, 146]

## Introduction

[cite_start]**GoPhish** is a powerful, open-source phishing framework used by security professionals to conduct simulated phishing campaigns and security awareness training[cite: 6]. [cite_start]It allows organizations to test their workforce for vulnerabilities by simulating real-world phishing attacks, tracking employee responses, and analyzing the results in a controlled environment[cite: 7]. [cite_start]This report documents the steps taken to set up and execute a simulated phishing attack using GoPhish on a Kali Linux Virtual Machine (VM)[cite: 9, 148].

---

## 1. GoPhish Setup and Access

[cite_start]The process began by either utilizing the pre-installed GoPhish tool in **Kali Linux** or downloading and installing the GoPhish release into the `/opt` directory[cite: 9, 153].

* [cite_start]The GoPhish server was started, and the initial **admin credentials** and server endpoints were logged[cite: 172, 199].
* [cite_start]The GoPhish web interface was accessed via the default browser, leading to the **Dashboard**[cite: 11, 15].



---

## 2. Campaign Configuration

The phishing simulation was configured in four main stages within the GoPhish administrative panel:

### 2.1. Sending Profile (SMTP)

[cite_start]A new **Sending Profile** was created to define the SMTP server details used to deliver the simulated emails[cite: 16].

* [cite_start]The required details like **Name**, **Interface Type**, **SMTP From** address, **Host**, **Username**, and **Password** were filled out[cite: 17, 18, 19, 20, 21, 22, 38].
* [cite_start]A **Test Email** was sent to verify the profile was working correctly, confirming the "Email Sent!" popup[cite: 28, 29, 39].



### 2.2. Landing Page

[cite_start]A deceptive **Landing Page** was set up to harvest credentials[cite: 40].

* [cite_start]A template for a Google Login page was chosen and its source code was copied into the Landing Page editor[cite: 45, 47].
* [cite_start]The **Redirect URL** was set to the legitimate Google accounts page, `https://accounts.google.com`, to make the process appear convincing after the victim submits their credentials[cite: 48].
* [cite_start]The page was saved as "Google Login"[cite: 49, 50].



### 2.3. Email Template

An **Email Template** was designed to lure the target into clicking the link.

* [cite_start]The content of a real email, specifically a **"2-Step Verification"** notice, was used as the basis for the template, pasted into the import email section[cite: 54, 110].
* [cite_start]A tracking link was embedded into the email content[cite: 106].

### 2.4. Users & Groups

[cite_start]A **User Group** was created to specify the target(s) of the campaign[cite: 58].

* [cite_start]A group named "shadow" was created, and the target's information (e.g., First Name: Black, Last Name: Shadow, Email: `shadowkernelscreamer@gmail.com`) was added[cite: 62, 71, 72, 66].



---

## 3. Campaign Launch and Monitoring

### 3.1. New Campaign

[cite_start]A **New Campaign** was created by combining all the prepared elements[cite: 78].

* [cite_start]The **Name**, **Email Template** (Google), **Landing Page** (Google Login), **URL** (Host IP address), and **User Group** (shadow) were all selected[cite: 75, 76].
* [cite_start]The campaign was launched, resulting in a **"Campaign Scheduled!"** confirmation[cite: 84, 90, 92].



### 3.2. Target Interaction

The simulation proceeded as follows:

1.  [cite_start]**Email Received:** The target received the email, which was a simulated "2-Step Verification turned on" notice[cite: 105, 110]. [cite_start]The target's mail client (Gmail) displayed a warning that the message might be dangerous[cite: 112].
2.  [cite_start]**Link Click:** The target clicked the link in the email and was redirected to the deceptive Google login page hosted on the attacker's IP address (e.g., `192.168.25.138`)[cite: 115, 117].
3.  **Credential Submission:** The target entered credentials on the fake login page. [cite_start]The credentials were captured by GoPhish, and the target was immediately redirected to their legitimate Google Account page, maintaining the illusion[cite: 118, 120].





### 3.3. Results Dashboard

[cite_start]The GoPhish dashboard instantly updated, showing the success of the simulation[cite: 94].

* [cite_start]The campaign statistics showed: **Emails Sent: 1**, **Emails Opened: 1**, **Clicked Link: 1**, and **Submitted Data: 1**[cite: 133, 134].
* [cite_start]The **Details** section provided a **Timeline** for the target user ("Black Shadow"), confirming the key steps: **Campaign Launched**, **Email Sent**, **Email Opened**, **Clicked Link**, and **Submitted Data**[cite: 128, 135].



---

## 4. Conclusion

[cite_start]This exercise successfully demonstrated how a **simulated phishing attack** is executed using the GoPhish framework[cite: 236]. The results highlight the potential vulnerability of a user who fails to:

1.  [cite_start]**Inspect the Sender Address:** The email came from a suspicious sender, not an official Google domain[cite: 111].
2.  [cite_start]**Verify the URL:** The landing page was hosted on an internal IP address, not the legitimate `accounts.google.com` domain[cite: 115].
3.  [cite_start]**Heed Security Warnings:** The target ignored the email client's explicit "This message might be dangerous" warning[cite: 112].

[cite_start]The successful capture of credentials (Submitted Data) underscores the necessity of ongoing **security awareness training** and the use of **Multi-Factor Authentication (MFA)** to prevent account compromise[cite: 7].