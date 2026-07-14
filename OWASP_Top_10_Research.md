# OWASP Top 10 Research — Cyber Security Internship, Week 1

**Name:** Muhammad Salman
**Track:** Cyber Security Internship
**Program:** Vortex Tech, Week 1 of 4

## Introduction

The OWASP Top 10 is the industry-standard list of the most critical security risks facing web applications. Below are five vulnerabilities from the list, explained in plain language along with how attackers exploit them, a real-world example, and how developers can prevent them.

---

## 1. Injection (e.g. SQL Injection)

**What it is**
Injection happens when an application takes user input and passes it directly into a command or query without checking it first. The most common form is SQL Injection, where an attacker sneaks database commands into a normal-looking input field, like a login box.

**How an attacker exploits it**
Imagine a login form that builds a database query by directly pasting in whatever the user types. If the app isn't careful, an attacker can type something like `' OR '1'='1` into the username field. Instead of being treated as a name, that text becomes part of the actual database command, tricking the system into logging them in without a real password, or worse, letting them read or delete data.

**Real-world example**
The 2017 Equifax breach, which exposed the personal data of roughly 147 million people, is often cited alongside injection-style attacks; the root cause there was an unpatched web framework vulnerability, but Equifax and similar breaches are frequently used as case studies for what happens when input isn't properly validated or systems aren't patched, since injection was rampant industry-wide around the same period. A cleaner and very well-documented case is the 2008 Heartland Payment Systems breach, where attackers used SQL injection to plant malware and steal over 130 million credit card numbers.

**Prevention**
Use parameterized queries (prepared statements) instead of building queries by joining strings together. This way, user input is always treated as data, never as a command.

---

## 2. Broken Authentication

**What it is**
This covers weaknesses in how an application verifies who a user is. If login, session, or password-recovery mechanisms are poorly built, attackers can impersonate other users.

**How an attacker exploits it**
Common tactics include credential stuffing (trying leaked username/password pairs from other breaches), brute-forcing weak passwords, or hijacking a session token that wasn't properly protected (for example, a token that never expires or is exposed in a URL).

**Real-world example**
In 2012, LinkedIn suffered a breach where 6.5 million hashed passwords were leaked; the hashing method used (unsalted SHA-1) was weak enough that attackers cracked a large portion of them quickly, exposing how fragile the authentication system's password storage was.

**Prevention**
Enforce multi-factor authentication (MFA), store passwords using strong salted hashing algorithms like bcrypt or Argon2, and set session tokens to expire and rotate regularly.

---

## 3. Cross-Site Scripting (XSS)

**What it is**
XSS occurs when an attacker manages to inject malicious JavaScript into a web page that other users then view. Because the browser trusts the site, it runs the attacker's script as if it belonged there.

**How an attacker exploits it**
A classic example is a comment box that doesn't sanitize input. An attacker posts a comment containing a hidden script tag. When another user loads the page, their browser silently executes that script, which could steal their session cookie or redirect them to a fake login page.

**Real-world example**
In 2014, a persistent XSS vulnerability was found in eBay's listing pages, where attackers embedded malicious scripts in item descriptions. Users viewing the compromised listings could be redirected to phishing pages designed to steal their eBay credentials.

**Prevention**
Sanitize and encode all user-generated content before displaying it, and use a Content Security Policy (CSP) header to restrict what scripts are allowed to run on the page.

---

## 4. Security Misconfiguration

**What it is**
This is a broad category covering systems that are left in an insecure state, default admin passwords never changed, unnecessary features left enabled, verbose error messages that leak internal details, or cloud storage left publicly accessible.

**How an attacker exploits it**
Attackers routinely scan the internet for exposed cloud storage buckets, admin panels still using default credentials, or servers revealing stack traces that hint at the underlying software and its version, then exploit any known weaknesses for that version.

**Real-world example**
In 2017, a misconfigured Amazon S3 storage bucket belonging to a Verizon partner exposed the personal data of around 14 million customers, because the bucket's access permissions were left open to the public instead of restricted.

**Prevention**
Follow a hardening checklist for every environment, disable unused features and default accounts, and regularly audit cloud storage and server permissions rather than assuming defaults are safe.

---

## 5. Vulnerable and Outdated Components

**What it is**
Modern applications are built on many third-party libraries and frameworks. If any of those components have a known vulnerability and aren't updated, the whole application inherits that weakness.

**How an attacker exploits it**
Attackers monitor public vulnerability databases for newly disclosed flaws in popular libraries, then scan the internet for applications still running the outdated, unpatched version, since patching is often slow across the industry.

**Real-world example**
The Equifax breach mentioned earlier is actually the clearest case for this category: attackers exploited a known vulnerability in the Apache Struts framework that had a patch available for months before the breach occurred, but Equifax had not applied it.

**Prevention**
Keep an inventory of all third-party components and their versions, subscribe to vulnerability alerts for the frameworks in use, and apply security patches promptly rather than deferring updates.

---

## Personal Reflection

The vulnerability that surprised me most was Security Misconfiguration, specifically how often massive breaches trace back to something as simple as a cloud storage bucket left public. It shows that a lot of security failures aren't caused by exotic, hard-to-execute attacks, but by basic settings nobody double-checked. It reinforced for me that consistent processes and checklists matter just as much as technical skill in preventing real damage.
