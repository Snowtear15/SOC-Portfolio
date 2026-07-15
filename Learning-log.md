***

<br>
## 2026-07-16 — THM: SOC Simulation : Splunk


**Time of activity:** Email Delivered 07/15/2026 21:26:08.853; User clicked malicious URL 07/15/2026 21:27:17.853

<br>
**List of Affected Entities:** user c.allen [c.allen@thetrydaily.thm], endpoint 10.20.2.25

<br>
**Reason for Classifying as True Positive:** Email impersonating microsoft by using typosquated email address [m1crosoftsupport.co] and linking mailicious credential harvesting links. Classic email phishing:: classified True Positive.

<br>
**Reason for Escalating the Alert:** firewall logs confirmed endpoint 10.20.2.25 accessing https://m1crosoftsupport.co/login, **Action**: allowed. High likelyhood of credential submission and account compromise.

<br>
**Recommended Remediation Actions:** Force password reset and session revoke for c.allen; block reported domain, ip address, email address and url at firewall. Purge mail form all inboxes; search mail logs for additional recipients of sender/domain. AV/EDR scan endpoint 10.20.2.25.

<br>
**List of Attack Indicators:** domain \[m1crosoftsupport\[\.\]co\]\, ip address \[45\.148\.10\.131\] \[102\.89\.222\.143\]\, url \[https://m1crosoftsupport\[\.\]co/login\]\, email address \[no\-reply@m1crosoftsupport\[\.\]co\]

***

## 2026-07-15 — THM: [SOC L1 Alert Reporting]

On Mar 27th, at 19:25, user Eddie Huffman received an email that was marked as phishing after an automated analysis was performed. The sender email address is support@microsoft.com. The tldr of the email was a '600% price increase in Microsoft teams pricing' and it ends with asking to 'download a report' for further information. There was an attached file 'REPORT.rar'. Given that there was a zip file attached and this was a spoofed email as SPF and DKIM were both failed, it has been reported as a phishing email.

<br>
On March 27th, at 19:56, a spike of several AD domain discovery related commands (whoami, net user, Get-ADUser) were detected running from a registered host 'DMZ-MSEXCHANGE-2013', host os 'Windows Server 2012 R2' by user 'SYSTEM'. Parent process of this activity was detected to be 'revshell.exe'. Given the grandparent process 'w2wp.exe' should never spawn a revshell or cmd shell access for any normal system activities, the machine is likely compromised and should be isolated. Escalating for further action.

> A w2wp exe is a core microsoft engine that helps in all IIS services, i.e., it handles all incoming Http requests and helps run web applications in isolation. IIS generates a w2wp exe instance for each webapp seperately so if a specific website's code crashes or freezes, it does not affect other websites. It should never use shell prompts or cmd on the local system. Detection of it doing so is likely a malicious actor has used it to install malware on the system.


