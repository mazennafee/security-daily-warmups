# Lesson: Social Engineering

## 📖 Source
- **Topic:** Social Engineering (The Human Element of Hacking)  
- **Context:** Cyber Security Fundamentals  
- **Date:** 2025-12-10  

---

## 🧠 Key Concepts
Social engineering refers to the manipulation of a user to make a mistake, such as sharing a password, opening a malicious file, or approving a fraudulent payment.  
The term “social” means the target is human beings, not computer systems. Attackers rely on psychological tricks to gain cooperation — hence the term *human hacking*.

### Phishing Variants
- **Phishing:** Fraudulent messages to steal credentials.  
- **Smishing:** Via SMS messages.  
- **Vishing:** Via voice calls.  
- **Quishing:** Via malicious QR codes.  

### Social Engineering Lifecycle / Kill Chain
1. **Reconnaissance:** Gathering information about the target.  
2. **Establish Trust / Develop Rapport:** Building legitimacy (pretexting).  
3. **Exploitation:** The user performs the desired action (e.g., clicking the link).  
4. **Disengagement:** Exiting without raising suspicion.  

---

## 🛠️ Attack Types & Delivery Mechanisms

| Attack Type            | Description                                                        | Channels Used       |
|------------------------|--------------------------------------------------------------------|---------------------|
| **Phishing**           | Mass distribution of fraudulent messages to steal credentials.     | Email, SMS, Phone   |
| **Spear Phishing**     | Highly targeted phishing referencing personal details.             | Email, LinkedIn     |
| **Pretexting**         | Invented scenario to obtain information (e.g., impersonating IT).  | Phone, In-person    |
| **Tailgating/Piggybacking** | Following an authorized person into restricted areas.         | Physical Access     |

---

## 🛠️ Technical Delivery: Social-Engineer Toolkit (SET)

SET is an open-source framework for simulating social engineering attacks, automating email delivery, and harvesting credentials.

### Core Command

```bash

   setoolkit

```
# Configuration Path for Mass Mailer Attack

## 📖 Steps
1. **Social-Engineering Attacks** → Select attack vector.  
2. **Mass Mailer Attack** → Email-based attack module.  
3. **E-Mail Attack Single Email Address** → Target a specific individual.  
4. **Use your own server or open relay** → Configure SMTP manually.  

---

## 🛠️ Critical Fields for Email Spoofing

| Field                  | Example Value               | Purpose                                      |
|------------------------|-----------------------------|----------------------------------------------|
| **Send email to**      | admin@company.com           | Target’s email address                       |
| **From address**       | markting@fcompany.com       | Spoofed sender (trusted vendor)              |
| **From name**          | admin                       | Displayed sender name                        |
| **SMTP server address**| smtp.company.com            | Mail server IP                               |
| **Email subject**      | Shipping Schedule Changes   | Urgent subject line                          |
| **Message body**       | http://CONNECTION_IP:8000 END | Narrative + malicious URL (trap)            |

---

## ⚡ Attack Flow for Credential Theft
1. **Setup Trap:** Host fake login page (e.g., `server.py` on port 8000).  
2. **Delivery via SET:** Send spoofed email with trap URL.  
3. **Exploitation:** Target enters credentials → harvested by server script.  

---

## 🔑 Psychological Drivers
Attackers exploit human psychology using principles of influence:

- **Urgency/Scarcity:** “Your account will be locked in 5 minutes!”  
- **Authority:** Requests from figures of power (CEO, IT admin).  
- **Curiosity/Liking:** Friendly persona or appealing subject lines.  
- **Consensus (Social Proof):** “Others have already complied.”  
- **Fear/Intimidation:** Threats of legal action or job loss.  

---

## 🚀 Observations & Defenses

### Anti-Phishing Mnemonics: **S.T.O.P.**

**Questions to Ask Before Acting:**
- Suspicious?  
- Telling me to click something?  
- Offering me an amazing deal?  
- Pushing me to act now?  

**Instructions to Follow:**
- **S**low down — scammers exploit adrenaline.  
- **T**ype the address yourself — don’t trust links.  
- **O**pen nothing unexpected — verify first.  
- **P**rove the sender — check the real address/number.  

---

### General Defenses
- **Verify Everything:** Use trusted channels (e.g., official phone numbers).  
- **Check the Sender:** Look for misspellings, hover over links.  
- **Be Suspicious of Emotion:** Fear, urgency, or excitement are red flags.  
- **Organizational Defenses:** Employee training, strict access control, least privilege.  

---

## 📌 References
- [CISA: Social Engineering and Phishing](https://www.cisa.gov/)  
- [SANS Institute: Social Engineering Attacks](https://www.sans.org/)  
- *The Art of Human Hacking* (book for deeper study)  
