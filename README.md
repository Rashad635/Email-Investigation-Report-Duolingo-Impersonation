# Email Investigation Report: Duolingo Impersonation

**Investigation Date:** October 5, 2026  
**Analyst:** Mohammed Rashad Abdallah  
**Classification:** Suspicious Brand Impersonation / Social Engineering  
**Severity:** Medium

---

## 1. Incident Overview

On **2025-07-13 at 15:50:03 UTC**, an email was delivered to `inquiry[@]mydfir[.]com` claiming to represent Duolingo and proposing a content collaboration.

The message identified the sender as:

- **Display name:** Duolingo
- **From:** `duolingo[.]ads[@]libero[.]it`

while directing replies to:

- **Reply-To:** `info[@]duolingo-team[.]com`

The message was transmitted through Libero/Italiaonline mail infrastructure and successfully passed SPF and DKIM validation for `libero[.]it`. These authentication results validate the sending infrastructure and DKIM signature associated with `libero[.]it`; they do **not** establish that the sender was an authorized representative of Duolingo.

The `duolingo-team[.]com` Reply-To domain is a significant indicator. WHOIS/domain-registration intelligence indicates that the domain was registered on **2025-07-10**, approximately three days before the email was delivered.

The message body contained a generic collaboration proposal from an individual identifying himself as **Roger Chapman**. No attachment or hyperlink was identified in the supplied `.eml` content.

Based on the available evidence, the email is assessed as **suspicious brand-impersonation/social-engineering activity**. The supplied artifact does not establish that the recipient clicked a link, opened an attachment, provided credentials, or experienced endpoint compromise.

**Reference:** See Appendix B for supporting email-header and authentication evidence.

---

## 2. Email Details

| **Field** | **Value** |
|---|---|
| Recipient | `inquiry[@]mydfir[.]com` |
| Display name | `Duolingo` |
| From | `duolingo[.]ads[@]libero[.]it` |
| Return-Path | `duolingo[.]ads[@]libero[.]it` |
| Reply-To | `info[@]duolingo-team[.]com` |
| Sender infrastructure | Italiaonline / Libero |
| Subject | `Join Us in Creating Unique Material` |
| Delivery time | `2025-07-13 15:50:03 UTC` |
| Authentication | SPF PASS, DKIM PASS |
| Attachments | None observed |
| URLs | None observed |
| Message-ID | `<0f5c8c2cbd890d58d8d4bf017977935b@smtp-34[.]iol[.]local>` |
| Date header | Missing |

**Reference:** See Appendix B, Section 1.

---

## 3. Mail Path

The observed mail flow was:

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
**Observed source IP**

90[.]160[.]50[.]35 was recorded in the Received: header as the connecting source for the SMTP submission to Libero infrastructure.

It should be treated as the observed SMTP submission source IP, rather than definitively identifying the physical sender or device.

**SMTP infrastructure**

The message was subsequently handled by:

- smtp-34[.]iol[.]local
- smtp-34[.]italiaonline[.]it
- srv7[.]swhc[.]ca

The public-facing Italiaonline SMTP server identified in the mail path was 213[.]209[.]10[.]34.

**Reference:** See Appendix B, Section 2.

---

## 4. Authentication Analysis

**SPF**

The email passed SPF validation:

- SPF: PASS

The SPF result indicates that the sending infrastructure was authorized by the SPF policy for the envelope sender domain:

- libero[.]it

The SPF evaluation therefore establishes authorization of the sending infrastructure for libero[.]it. It does not establish that the sender was affiliated with Duolingo.

The relevant distinction is:

SPF authentication:
- 213[.]209[.]10[.]34 → authorized for libero[.]it

Claimed organization:
- Duolingo

The authenticated domain and the claimed organization are therefore different.

**DKIM**

The message contained a valid DKIM signature associated with:

- d=libero[.]it
- s=s2021

The receiving system reported:

- DKIM_VALID
- DKIM_VALID_AU
- DKIM_VALID_EF
- DKIM_SIGNED

The DKIM signature therefore successfully validated against libero[.]it. This confirms that the message was cryptographically signed for the libero[.]it domain.

However, DKIM authentication does not establish that the sender was affiliated with Duolingo.

**Authentication assessment**

The authentication results demonstrate:

- SPF  → PASS
- DKIM → PASS

These results authenticate the libero[.]it sending identity and infrastructure. They do not authenticate the claimed Duolingo identity.

This distinction is important because a malicious actor can use a legitimate email service or a domain they control while successfully passing SPF and DKIM.

**Reference:** See Appendix B, Section 3.

---

## 5. Sender and Reply-To Analysis

The message presents three separate identity elements:

- Display name: Duolingo
- From: duolingo[.]ads[@]libero[.]it
- Reply-To: info[@]duolingo-team[.]com

The use of the Duolingo display name with a libero[.]it sender address is inconsistent with a typical corporate sender identity.

The Reply-To address is more significant because replies would be directed to:

- info[@]duolingo-team[.]com

The domain duolingo-team[.]com was registered on 2025-07-10, approximately three days before the observed email.

The timing is relevant to the investigation but does not independently identify the domain owner or prove malicious registration.

The combination of:

```text
Duolingo
      ↓
duolingo[.]ads[@]libero[.]it
      ↓
info[@]duolingo-team[.]com

```
creates a significant brand-impersonation concern.

**Reference:** See Appendix B, Section 4.

6. Content Analysis

The message states that the sender is Roger Chapman and claims to work at Duolingo.

The message describes the recipient as someone who actively shares content related to linguistic education and proposes a collaboration.

The message uses generic marketing and collaboration language and attempts to establish credibility through the Duolingo brand.

The supplied message does not contain a technical exploit, credential-harvesting link, or malicious attachment.

However, the social-engineering pretext is consistent with an attempt to establish communication with the recipient while presenting a potentially misleading organizational identity.

Reference: See Appendix B, Section 5.

7. Attachment Analysis

The email uses:

Content-Type: multipart/mixed

However, inspection of the supplied MIME content identified only a:

text/plain

message part.

No attachment was identified.

Therefore, there is no evidence from this artifact of malicious attachment delivery.

8. URL Analysis

No HTTP or HTTPS URLs were identified in the supplied message body.

There is therefore no malicious URL available for analysis from this artifact.

The following domain remains an indicator because it appears in the Reply-To address:

duolingo-team[.]com

This domain should be investigated separately through domain-registration, DNS, reputation, and historical threat-intelligence sources.

9. Spam Analysis

The SpamAssassin analysis reported:

SpamAssassin score: 1.2
Spam threshold: 50.0
Classification: Not spam

The message was therefore not classified as spam by the receiving mail system.

FREEMAIL_FROM

The SpamAssassin analysis identified the sender as originating from a freemail provider through the:

FREEMAIL_FROM

rule.

This rule did not contribute a positive score in the supplied analysis and should not independently be considered evidence of malicious activity.

MISSING_DATE

The message triggered the:

MISSING_DATE

rule because no standard Date: header was present.

The rule contributed:

1.4 points

to the spam analysis.

The absence of a Date: header is an email-format anomaly but does not independently establish malicious activity.

Reference: See Appendix B, Section 6.

10. Timeline
Timestamp (UTC)	Activity
2025-07-10	duolingo-team[.]com registered
2025-07-13 15:50:01	Message submitted through Italiaonline SMTP infrastructure
2025-07-13 15:50:03	Message accepted by srv7[.]swhc[.]ca
2025-07-13 15:50:03	Message delivered to inquiry[@]mydfir[.]com
11. 5 Ws and How
Who

The message claimed to originate from Duolingo.

The actual sender address was:

duolingo[.]ads[@]libero[.]it

The Reply-To address was:

info[@]duolingo-team[.]com

The message identified the sender as Roger Chapman.

What

A collaboration proposal was sent to the organization's inquiry mailbox using the Duolingo brand in the display name.

The message passed SPF and DKIM authentication for libero[.]it, while replies were directed to a separate domain associated with the claimed brand.

When

The email was delivered on:

2025-07-13 at 15:50:03 UTC

The Reply-To domain was registered approximately three days earlier, on:

2025-07-10
Where

The message was delivered to:

inquiry[@]mydfir[.]com

The observed sending infrastructure included:

90[.]160[.]50[.]35
213[.]209[.]10[.]34

The mail flow passed through Italiaonline/Libero infrastructure.

Why

The available evidence indicates that the message was intended to initiate communication while presenting itself as a Duolingo business collaboration.

The use of a non-Duolingo sender domain combined with a separate Reply-To domain creates a significant brand-impersonation concern.

The ultimate objective cannot be established from the supplied .eml alone.

How

The message appears to have been submitted through legitimate authenticated Libero/Italiaonline mail infrastructure.

The sender used the display name Duolingo while sending from libero[.]it and configured duolingo-team[.]com as the Reply-To destination.

This allowed the message to authenticate successfully against the actual sending domain while presenting a different organizational identity to the recipient.

12. Threat Intelligence Findings
12.1 Official Duolingo domain

The official Duolingo website is:

duolingo[.]com

This is the legitimate domain associated with Duolingo's language-learning services.

The email under investigation, however, used:

duolingo[.]ads[@]libero[.]it

as the sender and:

info[@]duolingo-team[.]com

as the Reply-To address.

The use of a separate duolingo-team[.]com domain to represent Duolingo is therefore a significant indicator requiring further investigation.

Official website:

https://www.duolingo.com/

Reference: See Appendix C, Section 1.

12.2 duolingo-team[.]com

Threat-intelligence research identified duolingo-team[.]com as a domain associated with reported phishing and scam activity involving impersonation of Duolingo.

Reported activity involving the domain describes a social-engineering approach in which malicious actors impersonate Duolingo and contact online content creators with fake collaboration or sponsorship opportunities.

Such campaigns may subsequently direct recipients to malicious files, including purported media kits or agreements, with the objective of obtaining credentials or compromising online accounts.

This finding is particularly relevant because the email under investigation uses:

Reply-To: info[@]duolingo-team[.]com
Subject: Join Us in Creating Unique Material

The Reply-To domain therefore aligns with the reported Duolingo impersonation pattern.

Reference: See Appendix C, Section 2.

12.3 libero[.]it

The sender address in the email was:

duolingo[.]ads[@]libero[.]it

The libero[.]it domain is a legitimate Italian email and web-services domain operated by Italiaonline S.p.A.

The domain has a long registration history, with domain creation recorded as:

1999-06-03

The domain itself should not be classified as malicious solely because it appears in the sender address.

The threat-intelligence results for the associated Libero infrastructure should therefore be interpreted in the context of the specific email rather than treating the entire libero[.]it domain as malicious.

Reference: See Appendix C, Section 3.

12.4 Sender IP: 90[.]160[.]50[.]35

The IP address 90[.]160[.]50[.]35 was identified in the email's Received: header as the connecting source for the SMTP submission to Libero infrastructure.

Threat-intelligence information from IPinfo classified the address as a public IP associated with a residential ISP network and geolocated it to Barcelona, Catalonia, Spain.

No VPN, proxy, Tor, relay, hosting, or residential-proxy classification was identified in the IP intelligence reviewed.

AbuseIPDB reported:

Abuse reports: 0
Abuse confidence score: 0%

The absence of AbuseIPDB reports does not establish that the IP is benign.

A public residential IP can be dynamically assigned to different customers, and an IP with no current reports may subsequently be associated with abusive activity.

The available intelligence therefore supports the conclusion that 90[.]160[.]50[.]35 is a publicly routable residential ISP address geolocated to Barcelona, Spain.

However, the IP intelligence does not establish the physical location or identity of the person who sent the email.

Reference: See Appendix C, Section 4.

12.5 Related Libero infrastructure: 213[.]209[.]17[.]209

Threat-intelligence research identified 213[.]209[.]17[.]209 as infrastructure associated with Italiaonline S.p.A. and the libero[.]it service.

This IP was not part of the observed mail path documented in Section 3. It is included here as related infrastructure identified during threat-intelligence research.

AbuseIPDB reported:

Reports: 9
Most recent report: approximately 2 years ago
ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Domain: italiaonline.it
Location: Milan, Lombardy, Italy

VirusTotal reported:

Detection: 1/91 security vendors

The single vendor detection should be treated as a reputation signal rather than definitive evidence that the IP or Libero service is malicious.

The infrastructure belongs to a legitimate email provider, and abuse reports associated with shared provider infrastructure may represent activity from individual customers rather than malicious activity by the provider itself.

Reference: See Appendix C, Section 5.

12.6 SMTP server: 213[.]209[.]10[.]34

The email header identifies 213[.]209[.]10[.]34 as the SMTP server that received the submission from 90[.]160[.]50[.]35:

Received: from [5.9.230.8] ([90.160.50.35])
    by smtp-34.iol.local with ESMTPSA

The subsequent mail-delivery hop identifies the public-facing infrastructure as:

smtp-34[.]italiaonline[.]it
213[.]209[.]10[.]34

Threat-intelligence results for this IP show:

AbuseIPDB reports: 10
Most recent report: approximately 2 months ago
ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Hostname: smtp-34[.]italiaonline[.]it
Domain: italiaonline.it
Location: Milan, Lombardy, Italy

The reports associated with 213[.]209[.]10[.]34 should be interpreted carefully because the IP is identified as legitimate Italiaonline SMTP infrastructure.

Abuse reports against shared mail infrastructure do not, by themselves, establish that the email under investigation was malicious or that Italiaonline participated in the activity.

Reference: See Appendix C, Section 6.

12.7 Overall threat-intelligence assessment

The strongest threat-intelligence indicator in this investigation is the duolingo-team[.]com Reply-To domain.

The domain is associated with reported Duolingo impersonation and phishing activity, and its use is consistent with the social-engineering theme of the email, which presents itself as a potential collaboration with Duolingo.

The sender's 90[.]160[.]50[.]35 IP does not currently have an abusive reputation in AbuseIPDB and is identified as a residential ISP address geolocated to Barcelona, Spain.

Consequently, the IP reputation does not independently support a malicious classification.

The libero[.]it infrastructure is associated with a legitimate Italian email provider. Although associated IP addresses have historical AbuseIPDB reports, those reports should not be interpreted as evidence that the provider itself is malicious.

Taken together, the threat-intelligence findings provide stronger evidence against the Reply-To domain and impersonation theme than against the underlying Libero infrastructure or sender IP.

The threat-intelligence assessment should therefore be correlated with the email's authentication results, message content, Reply-To relationship, URLs, attachments, domain registration history, and any subsequent communication before assigning a final incident classification.

13. MITRE ATT&CK
Technique ID	Technique Name	Assessment
T1684.001	Social Engineering: Impersonation	The sender used the Duolingo display name while using duolingo[.]ads[@]libero[.]it as the actual sender address and duolingo-team[.]com as the Reply-To domain. This is consistent with impersonation of a trusted organization.
T1566	Phishing	Potentially applicable. The email uses social-engineering content and a brand-impersonation pretext, but the supplied artifact contains no malicious attachment or hyperlink. The available evidence does not establish a specific phishing sub-technique.
14. Recommendations
Search the organization's mailboxes for:
duolingo-team[.]com
duolingo[.]ads[@]libero[.]it
info[@]duolingo-team[.]com
Determine whether other recipients received similar messages.
Search for replies sent to info[@]duolingo-team[.]com.
Search DNS, proxy, firewall, and EDR telemetry for connections to duolingo-team[.]com.
Search for subsequent messages from duolingo-team[.]com, especially messages containing attachments or links.
If the recipient interacted with the email, correlate the email timestamp with endpoint telemetry for browser activity, Outlook activity, PowerShell, command shell, script interpreters, process execution, and file creation.
Preserve the original .eml and record its SHA-256 hash as evidence.
Consider blocking or monitoring duolingo-team[.]com if additional evidence confirms malicious activity or repeated targeting.
Configure email security controls to evaluate display-name impersonation, Reply-To mismatches, and domain alignment rather than relying solely on SPF/DKIM pass results.
Review DMARC and anti-impersonation controls for protection against messages that authenticate successfully to unrelated domains while claiming another organization's identity.
15. Conclusion

The email successfully passed SPF and DKIM validation for libero[.]it, and the observed SMTP infrastructure is consistent with legitimate Libero/Italiaonline mail services.

These authentication results do not validate the claimed Duolingo identity.

The primary concern is the combination of:

The Duolingo display name
The libero[.]it sender address
The duolingo-team[.]com Reply-To address
The recent registration of duolingo-team[.]com before the email was delivered
Threat-intelligence reporting associating the Reply-To domain with Duolingo impersonation activity

The supplied email contains no attachment or hyperlink and provides no evidence of malware execution, credential submission, or endpoint compromise.

The available evidence therefore supports classifying the artifact as a suspicious brand-impersonation/social-engineering email, while further mailbox and endpoint correlation is required to determine whether the campaign resulted in user interaction or follow-on compromise.

Appendix A: Indicators of Interest
Email addresses
duolingo[.]ads[@]libero[.]it
info[@]duolingo-team[.]com
Domains
libero[.]it
duolingo-team[.]com
duolingo[.]com
italiaonline[.]it
IP addresses
90[.]160[.]50[.]35
213[.]209[.]10[.]34
213[.]209[.]17[.]209
Hostnames
smtp-34[.]iol[.]local
smtp-34[.]italiaonline[.]it
srv7[.]swhc[.]ca
Message ID
<0f5c8c2cbd890d58d8d4bf017977935b@smtp-34[.]iol[.]local>
Subject
Join Us in Creating Unique Material
Appendix B: Email Evidence
B.1 Relevant email headers
Return-Path: <duolingo.ads@libero.it>

Delivered-To: inquiry@mydfir.com

Received: from smtp-34.swhc.ca
    by srv7.swhc.ca with LMTP
    id qEJyG6vVc2jVPwQAe4cVtA
    (envelope-from <duolingo.ads@libero.it>)
    for <inquiry@mydfir.com>;
    Sun, 13 Jul 2025 11:50:03 -0400

Received: from smtp-34.italiaonline.it ([213.209.10.34]:46193 helo=libero.it)
    by srv7.swhc.ca with esmtps
    (TLS1.2)
    tls TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    (Exim 4.98.1)
    (envelope-from <duolingo.ads@libero.it>)
    id 1uayxm-00000001YyH-2ua6
    for inquiry@mydfir.com;
    Sun, 13 Jul 2025 11:50:03 -0400

Received: from [5.9.230.8] ([90.160.50.35])
    by smtp-34.iol.local with ESMTPSA
    id ayxjugAqkM7XtayxkuUeyF;
    Sun, 13 Jul 2025 17:50:01 +0200

DKIM-Signature: v=1;
    a=rsa-sha256;
    c=relaxed/relaxed;
    d=libero.it;
    s=s2021;
    t=1752421801;
    bh=7OXbSsYzwrYCLjKxSHNdvVQU8BqczR9BIZvyWZUPhS8=;
    h=From;
    b=...

Message-ID:
<0f5c8c2cbd890d58d8d4bf017977935b@smtp-34.iol.local>

Content-Type:
multipart/mixed

MIME-Version: 1.0

From:
Duolingo <duolingo.ads@libero.it>

To:
inquiry@mydfir.com

Subject:
Join Us in Creating Unique Material

Reply-To:
info@duolingo-team.com

X-Spam-Status:
No, score=1.2

X-Spam-Score:
12

X-Spam-Bar:
+

X-Spam-Flag:
NO
B.2 Mail-path interpretation
90[.]160[.]50[.]35
    │
    │ ESMTPSA
    ↓
smtp-34[.]iol[.]local
    │
    │ SMTP
    ↓
213[.]209[.]10[.]34
smtp-34[.]italiaonline[.]it
    │
    │ ESMTPS
    ↓
srv7[.]swhc[.]ca
    │
    │ LMTP
    ↓
inquiry[@]mydfir[.]com

The Received: headers indicate that the message was submitted through authenticated SMTP (ESMTPSA) to Italiaonline/Libero infrastructure before being delivered to the recipient mail server.

B.3 Authentication evidence

The receiving system reported successful authentication for the sender domain:

SPF: PASS
DKIM: PASS

The DKIM signature contained:

d=libero.it
s=s2021

The authentication results validate the libero[.]it sending identity and do not independently validate the claimed Duolingo identity.

B.4 Sender and Reply-To evidence
From:
Duolingo <duolingo.ads@libero.it>

Reply-To:
info@duolingo-team.com

This mismatch is relevant because the visible brand identity differs from both the sender and Reply-To domains.

B.5 Message content

The message stated:

Hello inquiry,

My name is Roger Chapman, and I work at Duolingo.

We noticed that you actively share content related to linguistic education, and we would like to propose a collaboration.

Our app helps millions of people learn languages, and we believe your influence could help increase awareness of our product.

We can offer you unique content and support for creating captivating pieces.

We would be happy to discuss this in more thoroughness!

Best regards,
Roger Chapman

No hyperlink or attachment was identified in the supplied MIME content.

B.6 SpamAssassin evidence

The receiving system reported:

X-Spam-Status: No, score=1.2

The detailed SpamAssassin analysis reported:

(1.2 points, 50.0 required)

The MISSING_DATE rule contributed:

1.4 points

The message was therefore classified as non-spam by the receiving system.

Appendix C: Threat Intelligence References
C.1 Official Duolingo domain
duolingo[.]com

The official Duolingo domain was used as the baseline for comparison with the sender and Reply-To domains.

C.2 duolingo-team[.]com

Domain-registration and threat-intelligence research identified the domain as associated with reported Duolingo impersonation/phishing activity.

The domain was registered on:

2025-07-10

The email was delivered on:

2025-07-13

This represents an approximately three-day interval between domain registration and email delivery.

C.3 libero[.]it

Domain information identifies libero[.]it as a legitimate domain operated by Italiaonline S.p.A.

Recorded domain creation:

1999-06-03

The domain should therefore not be treated as malicious solely because it was used in the sender address.

C.4 90[.]160[.]50[.]35

Threat-intelligence information reviewed:

IP type: Public IPv4
Network type: Residential ISP
Geolocation: Barcelona, Catalonia, Spain
VPN: Not identified
Proxy: Not identified
Tor: Not identified
Hosting: Not identified
AbuseIPDB reports: 0
Abuse confidence: 0%

The IP should not be treated as proof of the sender's physical identity or location.

C.5 213[.]209[.]17[.]209

Related Libero/Italiaonline infrastructure identified through threat-intelligence research:

ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Domain: italiaonline.it
Location: Milan, Lombardy, Italy
AbuseIPDB reports: 9
Most recent report: Approximately 2 years ago
VirusTotal detection: 1/91

This IP was not observed in the primary mail path.

C.6 213[.]209[.]10[.]34

Observed SMTP infrastructure:

Hostname: smtp-34[.]italiaonline[.]it
ISP: Italiaonline S.p.A.
Usage type: Fixed Line ISP
ASN: AS8660
Domain: italiaonline.it
Location: Milan, Lombardy, Italy
AbuseIPDB reports: 10
Most recent report: Approximately 2 months ago

Because the IP belongs to shared email-provider infrastructure, reputation results should be interpreted in context and should not independently be treated as evidence that the provider or the investigated email is malicious.

Appendix D: Analyst Assessment
Key findings
Finding	Assessment
SPF	PASS for libero[.]it
DKIM	PASS for libero[.]it
Claimed organization	Duolingo
Sender domain	libero[.]it
Reply-To domain	duolingo-team[.]com
Reply-To domain registration	2025-07-10
Email delivery	2025-07-13 15:50:03 UTC
Attachment	None observed
URL	None observed
Sender IP reputation	No current AbuseIPDB reports
Primary concern	Brand impersonation / social engineering
Confirmed endpoint compromise	Not established
Final assessment

Classification: Suspicious Brand Impersonation / Social Engineering

Confidence: Moderate

The evidence supports suspicion of brand impersonation and social-engineering activity, but the supplied email artifact alone does not establish malicious payload delivery, credential theft, user interaction, or endpoint compromise.
