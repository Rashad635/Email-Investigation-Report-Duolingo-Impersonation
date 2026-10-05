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
