***

<br>
## 2026-07-16 — THM: SOC Simulation : Splunk


**Time of activity:** Email delivered 07/15/2026 21:26:08; user clicked malicious URL 21:27:17 (firewall: allowed).

**Affected entities:** User c.allen ([c.allen@thetrydaily.thm](mailto:c.allen@thetrydaily.thm)); endpoint 10.20.2.25.
**TP rationale:** Inbound email impersonates Microsoft via typosquatted domain (m1crosoftsupport.co) with urgency pretext and credential-harvesting link. Classic phishing indicators; classified True Positive.
**Escalation rationale:** Firewall logs confirm endpoint 10.20.2.25 connected to hxxps://m1crosoftsupport[.]co/login (45.148.10.131) one minute after delivery, action **allowed** — high likelihood of credential submission and account compromise.
**Remediation:** Force password reset and revoke sessions for c.allen; block domain, URL, and IP at proxy/firewall; purge email from all mailboxes; search mail logs for additional recipients from sender/domain; AV/EDR scan endpoint 10.20.2.25.
**IOCs:** m1crosoftsupport[.]co · hxxps://m1crosoftsupport[.]co/login · 45.148.10.131 · [no-reply@m1crosoftsupport.co](mailto:no-reply@m1crosoftsupport.co)

<br>
***

## 2026-07-15 — THM: [SOC L1 Alert Reporting]

On Mar 27th, at 19:25, user Eddie Huffman received an email that was marked as phishing after an automated analysis was performed. The sender email address is support@microsoft.com. The tldr of the email was a '600% price increase in Microsoft teams pricing' and it ends with asking to 'download a report' for further information. There was an attached file 'REPORT.rar'. Given that there was a zip file attached and this was a spoofed email as SPF and DKIM were both failed, it has been reported as a phishing email.

<br>
On March 27th, at 19:56, a spike of several AD domain discovery related commands (whoami, net user, Get-ADUser) were detected running from a registered host 'DMZ-MSEXCHANGE-2013', host os 'Windows Server 2012 R2' by user 'SYSTEM'. Parent process of this activity was detected to be 'revshell.exe'. Given the grandparent process 'w2wp.exe' should never spawn a revshell or cmd shell access for any normal system activities, the machine is likely compromised and should be isolated. Escalating for further action.

> A w2wp exe is a core microsoft engine that helps in all IIS services, i.e., it handles all incoming Http requests and helps run web applications in isolation. IIS generates a w2wp exe instance for each webapp seperately so if a specific website's code crashes or freezes, it does not affect other websites. It should never use shell prompts or cmd on the local system. Detection of it doing so is likely a malicious actor has used it to install malware on the system.


