***

## 2026-07-15 — THM: [SOC L1 Alert Reporting]

On Mar 27th, at 19:25, user Eddie Huffman received an email that was marked as phishing after an automated analysis was performed. The sender email address is support@microsoft.com. The tldr of the email was a '600% price increase in Microsoft teams pricing' and it ends with asking to 'download a report' for further information. There was an attached file 'REPORT.rar'. Given that there was a zip file attached and this was a spoofed email as SPF and DKIM were both failed, it has been reported as a phishing email.

<br>
On March 27th, at 19:56, a spike of several AD domain discovery related commands (whoami, net user, Get-ADUser) were detected running from a registered host 'DMZ-MSEXCHANGE-2013', host os 'Windows Server 2012 R2' by user 'SYSTEM'. Parent process of this activity was detected to be 'revshell.exe'. Given the grandparent process 'w2wp.exe' should never spawn a revshell or cmd shell access for any normal system activities, the machine is likely compromised and should be isolated. Escalating for further action.

<br>
> A w2wp exe is a core microsoft engine that helps in all IIS services, i.e., it handles all incoming Http requests and helps run web applications in isolation. IIS generates a w2wp exe instance for each webapp seperately so if a specific website's code crashes or freezes, it does not affect other websites. It should never use shell prompts or cmd on the local system. Detection of it doing so is likely a malicious actor has used it to install malware on the system. 


<br>
