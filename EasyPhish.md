Phishing emails:

To understand phishing emails we need to understands the security protocols of emails such as DMARC, SPF and DKIM.

**SPF:**

Sender Policy Framework (SPF) restricts and provides secure DNS servers routings. This prevents domain spoofing by limiting the number of clients that are allowed to use your server domain domain. They keep a record of all the clients that uses your domain for smtp routing. 

**DKIM:**
DomainKeys Indentified Mail (DKIM) checks the sender details and the content of the email sent to verify if the email is sent from the correct user. It also checks if the email has been tampered with.

**DMARC:**
Domain-based Message Authentication, Reporting and Conformance (DMARC) combines both protocol from SPF and DKIM to check for consistency in the email. It lists the sender\`s domain name in the header.

Based on understanding these key feature of an email security protocol we needed to find a linux tool to checks those features of a dns. One such tool is called dig which is a built in linux command for queriying DNS name server.

**Steps:**
1. First we query using ('dig secure-startup.com') just to get the basic result and to check the spf records.
  * Here we find the DNS server in the record which is 34.102.136.180 which is not very useful in this case.
2. Now we query using TXT record for all the text record of the domain using ('dig TXT secure-startup.com').
  * Here we find part of the HTB flag which is 'HTB{RIP_SPF_Always_2nd' in the spf record under the ANSWER SECTION.
3. After findind the first part of the flag we need to test the DMARC of the of the server using the same TXT to check the text record using ('dig TXT secure-startup.com _dmarc.secure-startup.com').
  * Here we find the second part of the flag whihc is '_F1ddl3_2_DMARC}' in the DMARC record under the ANSWER SECTION.

Final Flag: HTB{RIP_SPF_Always_2nd_F1ddl3_2_DMARC
