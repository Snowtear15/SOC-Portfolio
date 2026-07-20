***

<br>
## 2026-07-16 — THM: SOC Simulation : Splunk

**Time of activity:** Email Delivered 07/15/2026 21:26:08.853; User clicked malicious URL 07/15/2026 21:27:17.853

When analysing any alert, follow the 5 steps below:

**The 5-step loop (same order, every alert, any type):**

1. **Read the alert rule + description first.** It literally tells you what to verify and often where to look — yours explicitly says "check firewall or proxy logs to determine whether any endpoints accessed the URLs." The alert description is your instruction sheet; half of staying un-lost is just doing what it says.
2. **Extract the entities.** Before forming any opinion, list the who/what/where: sender, recipient, timestamps, IPs, URLs/domains, hashes, hostnames. These are your pivot keys for every query you'll run. Here: sender domain `m1crosoftsupport.co`, recipient `c.allen@thetrydaily.thm`, the link `https://m1crosoftsupport.co/login`, IP `102.89.222.143`, timestamp \~21:26 on 07/15.
3. **Ask the verdict question: is the alerted behavior malicious, and did it succeed?** Two separate questions. For phishing: (a) is the email malicious? (b) did anyone click/credential-submit? For malware: is the file bad / did it execute? For login alerts: is it the real user / did they get in? Gather evidence for both before touching the classification buttons.
    * *Malicious?* Here, yes, textbook: typo squatted domain (`m1crosoft` — impersonating Microsoft), urgency pretext ("unusual sign-in"), credential-harvesting link disguised as "Review Activity," sender spoofing a security team. That settles True Positive.
    * *Succeeded?* You don't know yet — this is what the SIEM is for. Search proxy/firewall logs for the recipient's endpoint hitting `m1crosoftsupport.co` after 21:26. Allowed connection = user likely clicked = escalation + password reset territory. Blocked or no hits = contained, lower urgency.
4. **Classify + decide escalation based on evidence, not vibes.** True/false positive comes from step 3a; escalation usually hinges on 3b (impact). A malicious email nobody clicked is TP but often closable with blocking actions; a clicked one escalates.
5. **Write the report in the same fixed structure every time.** The sim's template is genuinely the industry pattern — reuse it forever: time of activity → affected entities → why TP/FP (cite specific evidence: "typo squatted domain impersonating Microsoft") → escalation rationale (what the proxy logs showed) → remediation (block sender domain, block URL at proxy, purge email from mailboxes, reset creds if clicked) → IOC list (domain, URL, IP, sender address).

***

<br>
**List of Affected Entities:** user c.allen [c.allen@thetrydaily.thm], endpoint 10.20.2.25

**Reason for Classifying as True Positive:** Email impersonating Microsoft by using typosquated email address [m1crosoftsupport.co] and linking malicious credential harvesting links. Classic email phishing:: classified True Positive.

**Reason for Escalating the Alert:** firewall logs confirmed endpoint 10.20.2.25 accessing https://m1crosoftsupport.co/login, **Action**: allowed. High likelyhood of credential submission and account compromise.

**Recommended Remediation Actions:** Force password reset and session revoke for c.allen; block reported domain, ip address, email address and url at firewall. Purge mail form all inboxes; search mail logs for additional recipients of sender/domain. AV/EDR scan endpoint 10.20.2.25.

**List of Attack Indicators:** domain \[m1crosoftsupport\[\.\]co\]\, ip address \[45\.148\.10\.131\] \[102\.89\.222\.143\]\, url \[https://m1crosoftsupport\[\.\]co/login\]\, email address \[no\-reply@m1crosoftsupport\[\.\]co\]

***

<br>
## 2026-07-15 — THM: [SOC L1 Alert Reporting]

On Mar 27th, at 19:25, user Eddie Huffman received an email that was marked as phishing after an automated analysis was performed. The sender email address is support@microsoft.com. The tldr of the email was a '600% price increase in Microsoft teams pricing' and it ends with asking to 'download a report' for further information. There was an attached file 'REPORT.rar'. Given that there was a zip file attached and this was a spoofed email as SPF and DKIM were both failed, it has been reported as a phishing email.

<br>
On March 27th, at 19:56, a spike of several AD domain discovery related commands (whoami, net user, Get-ADUser) were detected running from a registered host 'DMZ-MSEXCHANGE-2013', host os 'Windows Server 2012 R2' by user 'SYSTEM'. Parent process of this activity was detected to be 'revshell.exe'. Given the grandparent process 'w2wp.exe' should never spawn a revshell or cmd shell access for any normal system activities, the machine is likely compromised and should be isolated. Escalating for further action.

> A w2wp exe is a core microsoft engine that helps in all IIS services, i.e., it handles all incoming Http requests and helps run web applications in isolation. IIS generates a w2wp exe instance for each webapp seperately so if a specific website's code crashes or freezes, it does not affect other websites. It should never use shell prompts or cmd on the local system. Detection of it doing so is likely a malicious actor has used it to install malware on the system.


<br>
