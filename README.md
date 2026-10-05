# Email Investigation Report: Duolingo Impersonation

**Investigation Date:** October 5, 2026  
**Analyst:** Mohammed Rashad Abdallah  
**Classification:** Potential Phishing / Brand Impersonation  
**Severity:** Medium

## Incident Overview

On 2025 11:50:03 UTC, an email was delivered to inquiry[@]mydfir[.]com claiming to represent Duolingo and proposing a content collaboration.

The message identified the sender as:

- Duolingo (duolingo.ads[@]libero[.]it)

while directing replies to:

- info[@]duolingo-team[.]com 

The message was transmitted through Libero/Italiaonline mail infrastructure and successfully passed SPF and DKIM validation for libero[.]it. The authentication results therefore validate the sending infrastructure and DKIM signature associated with libero[.]it and do not establish that the sender was an authorized representative of Duolingo.

The duolingo-team[.]com  Reply-To domain is a significant indicator. VirusTotal information shows that the domain was registered on 2025-07-10, approximately three days before the email was delivered.

The message body contained a generic collaboration proposal from an individual identifying himself as Roger Chapman. No attachment or hyperlink was identified in the supplied .eml content.

Based on the available evidence, the email is assessed as suspicious brand-impersonation/social-engineering activity. The supplied artifact does not establish that the recipient clicked a link, opened an attachment, provided credentials, or experienced endpoint compromise.

## Email Details

| **Field** | **Value** |
|---|---|
| Recipient | `inquiry@mydfir.com` |
| Display name | `Duolingo` |
| From | `duolingo.ads@libero.it` |
| Return-Path | `duolingo.ads@libero.it` |
| Reply-To | `info@duolingo-team.com` |
| Sender infrastructure | Italiaonline / Libero |
| Subject | `Join Us in Creating Unique Material` |
| Delivery time | `2025-07-13 15:50:03 UTC` |
| Authentication | SPF PASS, DKIM PASS, DMARC not observed |
| Attachments | None observed |
| URLs | None observed |
| Message-ID | `<0f5c8c2cbd890d58d8d4bf017977935b@smtp-34.iol.local>` |
| Date header | Missing |

**Reference: See Appendix B, Section 1.**

## Mail Path

```text
90[.]160[.]50[.]35
        ↓
smtp-34[.]iol[.]local
        ↓
smtp-34[.]italiaonline[.]it / 213[.]209[.]10[.]34
        ↓
srv7[.]swhc[.]ca
        ↓
inquiry[@]mydfir[.]com

```
**Reference: See Appendix B, Section 2.**

## Authentication Analysis 

SPF returned: SPF_PASS

The result indicates that the sending infrastructure was authorized by the SPF policy for libero.it. The authenticated domain was libero[.]it, not duolingo domain (e.g. duolingo.com).

DKIM

The message contained a valid DKIM signature, signed by libero.it

The available results included:

DKIM_VALID
DKIM_VALID_AU
DKIM_VALID_EF
DKIM_SIGNED

The DKIM signature therefore validates against libero[.]it. And does not establish that the sender was affiliated with Duolingo. (See Appendix B, Section 3)

5. Sender And Reply-To Analysis 

The message presents three separate identity elements:

Duolingo
duolingo[.]ads@libero[.]it
info@duolingo-team[.]com 

The use of the Duolingo display name with a libero.it sender address is inconsistent with a typical corporate sender identity.

The Reply-To address is more significant because responses would be directed to duolingo-team[.]com .

The domain (duolingo-team[.]com) was registered on 2025-07-10, three days before the observed email. This timing is relevant to the investigation but does not independently identify the domain owner or prove malicious registration. (See Appendix B, Section 4)

6. Content Analysis 

The message states that the sender is Roger Chapman and claims to work at Duolingo.

The message describes the recipient as someone who actively shares linguistic-education content and proposes a collaboration.

The message contains generic marketing/collaboration language and attempts to establish credibility through the Duolingo brand. (See Appendix B, Section 5)

7. Attachment Analysis

The email uses:

Content-Type: multipart/mixed

However, the supplied MIME content contains only a text/plain message part.

No attachment was identified.

Therefore, there is no evidence from this artifact of malicious attachment delivery.

8. Url Analysis

No HTTP or HTTPS URLs were identified in the supplied message.

There is therefore no malicious URL available for analysis from this artifact.

The duolingo-team[.]com  domain remains an indicator because it appears in the Reply-To address.

9. Spam Analysis 

The SpamAssassin analysis reported a score of 1.2 against a threshold of 50.0 and classified the message as non-spam 

The SpamAssassin identified the sender as originating from a freemail provider through the FREEMAIL_FROM rule.

The message triggered the SpamAssassin MISSING_DATE rule because no standard Date: header was present in the message. The rule contributed 1.4 points to the spam analysis. The absence of a Date: header is an email-format anomaly but does not independently indicate malicious activity. (See Appendix B, Section 6)

10. Timeline

Timestamp (UTC)
Activity
2025-07-10
duolingo-team[.]com  registered
2025-07-13 15:50:01
Message submitted through Italiaonline SMTP infrastructure
2025-07-13 15:50:03
Message accepted by srv7[.]swhc[.]ca
2025-07-13 15:50:03
Message delivered to inquiry@mydfir.com



11. 5 Ws And How

Who:

The message claimed to originate from Duolingo.

The actual sender address was:

duolingo[.]ads@libero[.]it

The Reply-To address was:

info@duolingo-team[.]com 

The message identified the sender as Roger Chapman.

What:

A collaboration proposal was sent to the organization's inquiry mailbox using the Duolingo brand in the display name.

The message passed SPF and DKIM authentication for libero[.]it, while replies were directed to a separate domain associated with the claimed brand.

When:

The email was delivered on:

2025-07-13 at 15:50:03 UTC

The Reply-To domain was registered approximately three days earlier.

Where:

The message was delivered to:

inquiry@mydfir.com

The observed sending infrastructure included:

IP Address: 
213[.]209[.]10[.]34
90[.]160[.]50[.]35
The mail flow passed through Italiaonline/Libero infrastructure.

Why:

The available evidence indicates that the message was intended to initiate communication while presenting itself as a Duolingo business collaboration.

The use of a non-Duolingo sender domain combined with a separate Reply-To domain creates a significant brand-impersonation concern.

The ultimate objective cannot be established from the supplied .eml alone.

How:

The message appears to have been submitted through legitimate authenticated Libero/Italiaonline mail infrastructure.

The sender used the display name Duolingo while sending from libero[.]it and configured duolingo-team[.]com  as the Reply-To destination.

This allowed the message to authenticate successfully against the actual sending domain while presenting a different organizational identity to the recipient.

12. Threat Intelligence Findings

Official Duolingo domain

The official Duolingo website is duolingo.com, which is the legitimate domain associated with Duolingo's language-learning services.

The email under investigation, however, used duolingo[.]ads@libero[.]it as the sender and info@duolingo-team[.]com as the Reply-To address. The use of a separate duolingo-team[.]com domain to represent Duolingo is therefore a significant indicator requiring further investigation.

Official Duolingo website: https://www.duolingo.com/ (See Appendix C, Section 1)

duolingo-team[.]com

Threat-intelligence research identified duolingo-team[.]com as a domain associated with phishing and scam activity involving impersonation of Duolingo.

Reported activity involving the domain describes a social-engineering approach in which malicious actors impersonate Duolingo and contact online content creators with fake collaboration or sponsorship opportunities. These campaigns may subsequently direct recipients to malicious files, including purported media kits or agreements, with the objective of obtaining credentials or compromising online accounts.

This finding is particularly relevant because the email under investigation uses:

Reply-To: info@duolingo-team[.]com
Subject: Join Us in Creating Unique Material

The Reply-To domain therefore aligns with the reported Duolingo impersonation pattern. (See Appendix C, Section 2)

libero[.]it

The sender address in the email was:

duolingo[.]ads@libero[.]it

The libero.it domain is a legitimate Italian email and web-services domain operated by Italiaonline S.p.A. The domain itself has a long registration history (Created on 1999-06-03) and should not be classified as malicious solely because it appears in the sender address.

The threat-intelligence results for the associated Libero infrastructure should therefore be interpreted in the context of the specific email rather than treating the entire libero.it domain as malicious. (See Appendix C, Section 3)

Sender IP: 90[.]160[.]50[.]35

The IP address 90[.]160[.]50[.]35 was identified in the email's Received: header as the connecting source for the SMTP submission to Libero infrastructure.

Threat-intelligence information from IPinfo classified the address as a public IP associated with a residential ISP network and geolocated it to Barcelona, Catalonia, Spain.

No VPN, proxy, Tor, relay, hosting, or residential-proxy classification was identified in the IP intelligence reviewed.

AbuseIPDB currently reports:

Abuse reports: 0
Abuse confidence score: 0%

The absence of AbuseIPDB reports does not establish that the IP is benign. A public residential IP can be dynamically assigned to different customers, and an IP with no current reports may subsequently be associated with abusive activity.

The available intelligence therefore supports the conclusion that 90[.]160[.]50[.]35 is a publicly routable residential ISP address geolocated to Barcelona, Spain, but it does not establish the physical location or identity of the person who sent the email. (See Appendix C, Section 4)

Libero infrastructure: 213[.]209[.]17[.]209

Threat-intelligence research identified 213[.]209[.]17[.]209 as infrastructure associated with Italiaonline S.p.A. and the libero[.]it service.

AbuseIPDB currently shows:

Reports: 9
Most recent report: approximately 2 years ago
ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Domain: italiaonline.it
Location: Milan, Lombardy, Italy

VirusTotal currently shows:

Detection: 1/91 security vendors

The single vendor detection should be treated as a reputation signal rather than definitive evidence that the IP or Libero service is malicious. The infrastructure belongs to a legitimate email provider, and abuse reports associated with shared provider infrastructure may represent activity from individual customers rather than maliciousness of the provider itself. (See Appendix C, Section 5)

SMTP server: 213[.]209[.]10[.]34

The email header identifies 213[.]209[.]10[.]34 as the SMTP server that received the submission from 90[.]160[.]50[.]35:

Received: from [5.9.230.8] ([90[.]160[.]50[.]35])
    by smtp-34[.]iol[.]local with ESMTPSA

The subsequent mail-delivery hop identifies the public-facing infrastructure as:

smtp-34[.]italiaonline[.]it 213[.]209[.]10[.]34

Threat-intelligence results for this IP show:

AbuseIPDB reports: 10
Most recent report: approximately 2 months ago
ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Hostname: smtp-34[.]italiaonline[.]it
Domain: italiaonline.it
Location: Milan, Lombardy, Italy

The reports associated with 213[.]209[.]10[.]34 should be interpreted carefully because the IP is identified as legitimate Italiaonline SMTP infrastructure. Abuse reports against shared mail infrastructure do not, by themselves, establish that the email under investigation was malicious or that Italiaonline participated in the activity. (See Appendix C, Section 6)

Overall threat-intelligence assessment

The strongest threat-intelligence indicator in this investigation is the duolingo-team[.]com Reply-To domain. The domain is associated with reported Duolingo impersonation and phishing activity, and its use is consistent with the social-engineering theme of the email, which presents itself as a potential collaboration with Duolingo.

The sender's 90[.]160[.]50[.]35 IP does not currently have an abusive reputation in AbuseIPDB and is identified as a residential ISP address geolocated to Barcelona, Spain. Consequently, the IP reputation does not independently support a malicious classification.

The libero.it infrastructure is associated with a legitimate Italian email provider. Although associated IP addresses have historical AbuseIPDB reports, those reports should not be interpreted as evidence that the provider itself is malicious.

Taken together, the threat-intelligence findings provide stronger evidence against the Reply-To domain and impersonation theme than against the underlying Libero infrastructure or the sender IP.

The threat-intelligence assessment should therefore be correlated with the email's authentication results, message content, Reply-To relationship, URLs, attachments, domain registration history, and any subsequent communication before assigning a final incident classification.


13. MITRE ATT&CK

Technique ID
Technique Name
Activity
T1684.001
Social Engineering: Impersonation
The use of the Duolingo display name with duolingo[.]ads@libero[.]it as the sender address.
T1566
Phishing
The email is consistent with social-engineering activity, but the supplied artifact contains neither a malicious attachment nor a malicious hyperlink.



14. Recommendations

Search the organization's mailboxes for:
duolingo-team[.]com
duolingo[.]ads@libero[.]it
info@duolingo-team[.]com .
Determine whether other recipients received similar messages.
Search for replies sent to info@duolingo-team[.]com.
Search DNS, proxy, firewall, and EDR telemetry for connections to duolingo-team[.]com.
Search for subsequent messages from duolingo-team[.]com, especially messages containing attachments or links.
If the recipient interacted with the email, correlate the email timestamp with endpoint telemetry for browser, Outlook, PowerShell, command shell, script interpreters, execution, and file creation activity.
Preserve the original .eml and record its SHA-256 hash as evidence.
Consider blocking or monitoring duolingo-team[.]com  if additional evidence confirms malicious activity or repeated targeting.
Configure email security controls to evaluate display-name impersonation, Reply-To mismatches, and domain alignment rather than relying solely on SPF/DKIM pass results.
Review DMARC and anti-impersonation controls for protection against messages that authenticate successfully to unrelated domains while claiming another organization's identity.
15. Conclusion

The email successfully passed SPF and DKIM validation for libero[.]it, and the observed SMTP infrastructure is consistent with legitimate Libero/Italiaonline mail services. These authentication results do not validate the claimed Duolingo identity.

The primary concern is the combination of the Duolingo display name, the libero.it sender address, and the duolingo-team[.]com  Reply-To address. The Reply-To domain was registered three days before the email was delivered, providing additional contextual evidence for suspicion.

The supplied email contains no attachment or hyperlink and provides no evidence of malware execution, credential submission, or endpoint compromise.

The available evidence therefore supports classifying the artifact as a suspicious brand-impersonation/social-engineering email, while further mailbox and endpoint correlation is required to determine whether the campaign resulted in user interaction or follow-on compromise.

























Appendix A: Indicators of Interest

Email addresses:
duolingo[.]ads@libero[.]it
info@duolingo-team[.]com 

Domains:
libero[.]it
duolingo-team[.]com 

IP addresses:
90[.]160[.]50[.]35
213[.]209[.]10[.]34

Hostname:
smtp-34[.]italiaonline[.]it

Message ID:
<0f5c8c2cbd890d58d8d4bf017977935b@smtp-34[.]iol[.]local>

Subject:
Join Us in Creating Unique Material
