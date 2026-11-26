 # DAY 1 — SECURITY FUNDAMENTALS
## SOC Analyst L1 Roadmap — Phase 1, Week 1

---

# 1. CYBERSECURITY

**Definition:** Cybersecurity is the practice of protecting computers, networks, systems and digital data from cyberattacks and unauthorized access.

**Simple meaning:** Protecting digital systems from hackers and attacks.

**Example:** Using a firewall to protect a company's network from unauthorized access.

# 2. INFORMATION SECURITY (INFOSEC)

**Definition:** Information Security is the practice of protecting information from unauthorized access, modification, disclosure or destruction.

It protects information in both digital and physical formats.

**Example:**
- Protecting customer information stored in a database.
- Locking confidential paper documents in a cabinet.

**Cybersecurity vs Information Security**

| Cybersecurity | Information Security |
|---|---|
| Protects digital systems and data from cyber threats | Protects information in all forms |
| Focuses on computers, networks and digital assets | Focuses on digital and physical information |
| Example: Firewall protection | Example: Securing paper documents |

**Important:** Cybersecurity is a part of the broader field of Information Security.

---

# 3. BASIC SECURITY TERMINOLOGY

## 3.1 Asset

**Definition:** An asset is anything valuable to an organization that needs protection.

Examples:
- Customer database
- Company laptop
- Employee accounts
- Servers
- Business information

**SOC example:** A company's customer database is an important asset.

## 3.2 Threat

**Definition:** A threat is anything that has the potential to cause harm to an asset.

Examples:
- Hackers
- Malware
- Phishing attacks
- Malicious insiders
- Ransomware

**SOC example:** An attacker attempting to steal customer information is a threat.

## 3.3 Vulnerability

**Definition:** A vulnerability is a weakness in a system, network or application that an attacker could exploit.

Examples:
- Weak passwords
- Outdated software
- Unpatched operating systems
- Misconfigured servers

**SOC example:** A server running outdated software with a known security flaw.

## 3.4 Exploit

**Definition:** An exploit is a method, technique or piece of code used to take advantage of a vulnerability.

Examples:
- Using an SQL injection flaw.
- Taking advantage of an unpatched software vulnerability.

**SOC example:** An attacker uses an SQL injection vulnerability to access unauthorized database records.

## 3.5 Risk

**Definition:** Risk is the possibility of harm or loss when a threat takes advantage of a vulnerability.

A simplified risk model is:

Risk = Likelihood × Impact

This is a simplified conceptual model, not a universal risk calculation formula.

**Example:**
- Asset: Company database
- Threat: Hacker
- Vulnerability: Weak password
- Exploit: Attacker uses the weak password to gain access
- Risk: Customer data may be stolen, causing financial and reputational damage.

### Easy way to remember

| Term | Meaning |
|---|---|
| Asset | What we protect |
| Threat | What can harm it |
| Vulnerability | Weakness |
| Exploit | Method used to take advantage of weakness |
| Risk | Potential damage or loss |

---

# 4. SECURITY CONTROLS

**Definition:** Security controls are safeguards used to protect assets and reduce security risks.

There are three basic types:

## 4.1 Preventive Controls

**Purpose:** Stop attacks before they happen.

Examples:
- Multi-Factor Authentication (MFA)
- Firewall
- Strong password policy
- Access restrictions

**SOC example:** MFA prevents an attacker from logging in using only a stolen password.

## 4.2 Detective Controls

**Purpose:** Identify suspicious activities or security incidents.

Examples:
- SIEM alerts
- Security monitoring
- Log analysis
- Intrusion Detection Systems (IDS)

**SOC example:** A SIEM detects repeated failed login attempts and generates an alert.

## 4.3 Corrective Controls

**Purpose:** Fix problems and help systems recover after an incident.

Examples:
- Resetting compromised passwords
- Restoring backups
- Removing malware
- Applying security patches

**SOC example:** After confirming account compromise, the security team resets credentials and helps restore secure access.

### Memory trick

- Preventive = STOP
- Detective = DETECT
- Corrective = FIX

---

# 5. CIA TRIAD

The CIA Triad is a fundamental model of Information Security.

CIA stands for:

1. Confidentiality
2. Integrity
3. Availability

## 5.1 Confidentiality

**Definition:** Ensures that information is accessible only to authorized people.

**Example:** Only authorized HR employees can access salary records.

**Possible security controls:** Encryption, access control and MFA.

## 5.2 Integrity

**Definition:** Ensures that information remains accurate, complete and protected from unauthorized modification.

**Example:** An attacker must not secretly change a bank account balance.

**Possible security controls:** Hashing, digital signatures and access controls.

## 5.3 Availability

**Definition:** Ensures that systems and information are accessible when required by authorized users.

**Example:** A hospital's patient management system should remain available to doctors.

**Possible security controls:** Backups, redundancy and DDoS protection.

### CIA Triad Memory Trick

- Confidentiality = Secret
- Integrity = Correct
- Availability = Accessible

---

# 6. AUTHENTICATION

**Definition:** Authentication is the process of verifying the identity of a user or system.

**Simple meaning:** Proving who you are.

Examples:
- Username and password
- OTP
- Fingerprint
- Face recognition

**SOC example:** An employee enters their username and password to log into a company system.

---

# 7. AUTHORIZATION

**Definition:** Authorization determines what an authenticated user is permitted to access or perform.

**Simple meaning:** Deciding what you are allowed to do.

Example:
- Employee: Can view company files.
- Administrator: Can view, edit and delete authorized records.

**SOC example:** An employee tries to access an administrator-only folder. Access controls should deny the request.

---

# 8. AUDITING

**Definition:** Auditing is the process of recording and reviewing activities to determine what happened, when it happened and who performed the activity.

Examples:
- Login records
- File access logs
- Account changes
- Administrative activities

**SOC example:** An analyst reviews login logs to determine who accessed an account at 2:15 AM.

---

# 9. AUTHENTICATION vs AUTHORIZATION vs AUDITING

| Concept | Meaning | Example |
|---|---|---|
| Authentication | Who are you? | Password or OTP |
| Authorization | What can you access? | Permission to view a file |
| Auditing | What did you do? | Reviewing activity logs |

**Remember:**
Authentication → Identity
Authorization → Permissions
Auditing → Activity records

---

# 10. SOC ANALYST L1 REAL-WORLD EXAMPLE

## Scenario: Suspicious Login Alert

A SIEM generates an alert with the following details:

- Username: employee01
- Asset: Company laptop
- Activity: Suspicious login
- Location: Unknown location
- Failed login attempts: 15
- Successful logins: 1
- Time: 02:15 AM

### How an L1 analyst thinks

1. Identify the affected asset and account.
2. Check the login timestamps and source IP.
3. Review authentication logs.
4. Check whether the successful login was legitimate.
5. Look for unusual account or device activity.
6. Escalate if compromise is suspected or confirmed.

**Important:** Multiple failed attempts followed by a successful login are suspicious, but do not automatically prove account compromise. Validate the evidence.

---

# 11. INTERVIEW QUESTIONS AND ANSWERS

**Q1. What is cybersecurity?**

Cybersecurity is the practice of protecting computers, networks, systems and digital data from cyberattacks.

**Q2. What is Information Security?**

Information Security protects information from unauthorized access, modification, disclosure or destruction in both digital and physical forms.

**Q3. What is an asset?**

An asset is anything valuable to an organization that needs protection, such as a laptop, server or database.

**Q4. What is a threat?**

A threat is anything that has the potential to cause harm to an asset.

**Q5. What is a vulnerability?**

A vulnerability is a weakness in a system or application that an attacker could exploit.

**Q6. What is an exploit?**

An exploit is a method or code used to take advantage of a vulnerability.

**Q7. What is risk?**

Risk is the possibility of harm or loss when a threat exploits a vulnerability.

**Q8. What are security controls?**

Security controls are safeguards used to protect assets and reduce security risks.

**Q9. What are the three types of security controls?**

Preventive, Detective and Corrective.

**Q10. What is the CIA Triad?**

The CIA Triad is a fundamental Information Security model consisting of Confidentiality, Integrity and Availability.

**Q11. What is authentication?**

Authentication verifies the identity of a user or system.

**Q12. What is authorization?**

Authorization determines what an authenticated user is allowed to access or perform.

**Q13. What is auditing?**

Auditing involves recording and reviewing activities to understand what happened and who performed them.

---

# 12. QUICK REVISION — ONE-MINUTE RECAP

Cybersecurity = Protect digital systems.

Information Security = Protect information in all forms.

Asset = What we protect.

Threat = What can cause harm.

Vulnerability = Weakness.

Exploit = Method used to take advantage of a weakness.

Risk = Possibility of damage.

Preventive = Stop.

Detective = Detect.

Corrective = Fix.

Confidentiality = Secret.

Integrity = Correct.

Availability = Accessible.

Authentication = Who are you?

Authorization = What can you access?

Auditing = What did you do?

---

