# SIEM Simulation 1 [THM]

**List of Affected Entities:** user c.allen [c.allen@thetrydaily.thm], endpoint 10.20.2.25

**Reason for Classifying as True Positive:** Email impersonating microsoft by using typosquated email address [m1crosoftsupport.co] and linking mailicious credential harvesting links. Classic email phishing:: classified True Positive.

**Reason for Escalating the Alert:** firewall logs confirmed endpoint 10.20.2.25 accessing https://m1crosoftsupport.co/login, **Action**: allowed\. High likelyhood of credential submission and account compromise\.\!\[1784154298122\_image\.png\.png\]\(/files/Soc\-Portfolio/attachments/1784154304622\_1784154298122\_image\.png\.png\)

**Recommended Remediation Actions:** Force password reset and session revoke for c.allen; block reported domain, ip address, email address and url at firewall. Purge mail form all inboxes; search mail logs for additional recipients of sender/domain. AV/EDR scan endpoint 10.20.2.25.

**List of Attack Indicators:** domain \[m1crosoftsupport\[\.\]co\]\, ip address \[45\.148\.10\.131\] \[102\.89\.222\.143\]\, url \[https://m1crosoftsupport\[\.\]co/login\]\, email address \[no\-reply@m1crosoftsupport\[\.\]co\]

![image.png](/files/Soc-Portfolio/attachments/1784154298122_image.png.png)
![image.png](/files/Soc-Portfolio/attachments/1784154330453_image.png.png)