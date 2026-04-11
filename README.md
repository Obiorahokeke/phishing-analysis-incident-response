# Case Study: Phishing Analysis - Incident Response

## Objective
Conducted a technical investigation of a suspicious "Microsoft" security alert to identify potential threats and determine the legitimacy of communication.

---

## Methodology & Key Findings

### 1. Indicators of Compromise (IoC) Identification
* **Sender Address:** Flagged a critical discrepancy between the branding (Microsoft Security Team) and the actual sending infrastructure (`info@libreriacies[.]es`).
* **TLD Anomaly:** The `.es` (Spain) TLD for a "Microsoft" email is a high-confidence IoC. Official alerts originate from verified domains like `@accountprotection.microsoft.com`.
* **Malicious URL:** Identified the use of a URL shortener (`tinyurl[.]com`) used to mask the final destination and bypass automated email filters.
* **Psychological Trigger:** Recognized social engineering tactics, including artificial urgency ("within 24 hours") and threats of account suspension.

### 2. Technical Domain & URL Analysis
* **MxToolbox Verification:** Analyzed the sender IP `217.18.163.139`. Identified `libreriacies[.]es` as a **legitimate but compromised asset**.
* **Authentication Weaponization:** The attacker leveraged the bookstore's valid SPF/DKIM configuration to deliver a fraudulent payload that appears technically "clean" to basic scanners.
* **VirusTotal Validation:** Performed a multi-engine scan of the embedded TinyURL. The link was flagged as **Malicious/Phishing** by multiple security vendors.

### 3. Evidence Screenshots

#### Original Phishing Email Analysis
![Phishing Email](phishing_email.jpg)

#### MxToolbox Reputation Results
![MxToolbox Analysis](mxtoolbox_result.jpg)

#### VirusTotal Analysis
![VirusTotal Scan](virustotal_url_result.jpg)

---

## Lessons Learned & Prevention Strategies

### 1. The Value of Multi-Tool Verification
This case proved that relying on a single security scanner is insufficient. While the sender's domain had a "Neutral" reputation in some databases (due to it being a hijacked legitimate business), **VirusTotal** and **MxToolbox** together revealed the underlying threat. 

### 2. User Awareness is the First Line of Defense
The attack utilized high-pressure social engineering ("24-hour deadline"). This reinforces the need for ongoing **Security Awareness Training (SAT)** to teach users how to spot "Urgency" as a red flag, regardless of how "official" an email looks.

### 3. Verification of "Official" Domains
Always cross-reference the sender with known official documentation. Microsoft explicitly lists their alert domains; any deviation (like a bookstore in Spain) should be treated as high-risk by default.

---

## Conclusion & Recommendations
**Classification:** `Confirmed Phishing Incident (Credential Harvesting)`

The attacker's goal was to lure the user to a fraudulent Microsoft login page to steal credentials. This represents a sophisticated attempt to exploit the trust of an established business infrastructure.

### SOC Recommendations:
1. **Immediate Deletion:** Remove the malicious email from the user's inbox.
2. **Domain Blocking:** Block the sender domain at the organizational gateway.
3. **URL Reporting:** Report the malicious TinyURL to the service provider's abuse team for takedown.
   
