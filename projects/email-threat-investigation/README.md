# Email Threat Investigation

I analysed 13 recovered emails from a fictional finance executive's mailbox, a training scenario from the Cryptonic Area Cybersecurity & Ethical Hacking Internship Program. For each email, I checked the sender, authentication results, links, attachments and social-engineering tactics, then classified it as safe, medium risk or suspicious.

> **Scope and attribution:** the company, people and emails are fictional and were supplied by the Cryptonic Area internship programme. Nothing here comes from a real organisation. The analysis and judgements are my own. The programme ended in August 2026, and the organiser stated that programme work could be made public after the internship, so I am publishing only my own analysis. I did not open any links or attachments, and all links below are defanged.

## Objective

Decide whether each of the 13 emails is legitimate or malicious using technical evidence and social-engineering indicators, and recommend what the recipient and the organisation should do.

## Environment and tools

- **Evidence:** The 13 emails as supplied, with their header summaries (From, Reply-To, Return-Path, Received From, SPF, DKIM, DMARC and TLS results), bodies, links and attachment names.
- **Method of work:** Manual review of every email. No tools were needed beyond manual review.

## Method

1. Compare the From, Reply-To and Return-Path addresses, and the server the email was received from.
2. Check SPF, DKIM, DMARC and TLS results, and note which domain each result applies to.
3. Compare each sender domain with the organisation's real domain, looking for look-alike and typosquatted names.
4. Inspect links (defanged) and attachment types for risk.
5. Read the body for social-engineering techniques: urgency, authority, fear, secrecy, reward and requests for credentials or money.
6. Classify the email, explain the reasoning, and state the impact and the recommended action.
7. Collect indicators of compromise (IOCs) in one table.

## Results

**Overall:** 5 safe, 2 medium risk, 6 suspicious.

| # | Email | Classification | Key evidence |
|---|---|---|---|
| 01 | Password expiry reminder | Safe | SPF, DKIM and DMARC pass; headers consistent; no links; tells users never to share passwords |
| 02 | Mailbox full, verify now | Suspicious | Look-alike sender domain; Reply-To and Return-Path go to a different domain; authentication fails; no TLS; credential-harvesting link |
| 03 | Invoice and new bank details | Medium risk | Authentication passes, but the email moves future payments to a new account and the Reply-To uses a different domain |
| 04 | Leave policy update | Safe | Authentication passes; consistent headers; no links or attachments |
| 05 | Confidential wire transfer | Suspicious | "Managing Director" writing from a look-alike domain; no SPF, DKIM or DMARC; free relay; secrecy and urgency (BEC) |
| 06 | Google Drive file share | Safe (verify before opening) | Sent from Google's infrastructure; authentication passes; link goes to docs.google.com |
| 07 | Microsoft sign-in alert | Suspicious | Typosquatted domain (zero instead of "o"); authentication fails; sent via a VPN exit node; credential link |
| 08 | Recruiter job offer | Medium risk | SPF and DKIM pass, but unsolicited offer, urgent reply, request for salary slip and ID, ZIP attachment, no DMARC policy |
| 09 | Software renewal invoice | Safe | Authentication passes; states no bank details changed; invoice should still be checked against records |
| 10 | Lottery prize | Suspicious | Generic mail domain; mismatched Reply-To; authentication fails; fee and personal-data request |
| 11 | CFO gift cards | Suspicious | Passes authentication, but Reply-To goes to a personal Outlook address; gift-card request; 20-minute deadline; "don't call" |
| 12 | Security training reminder | Safe | Authentication passes; no links; points to the internal learning portal |
| 13 | Pending invoice | Suspicious | SPF and DMARC fail; no DKIM; unrelated hosting server; macro-enabled .docm; deceptive link domain |

### What I learned from the hard cases

- **Email 11 shows that passing authentication isn't enough.** SPF, DKIM and DMARC all passed, yet it is a gift-card fraud. The Reply-To sends answers to a personal address, and the request, urgency and "don't call" instruction are classic business email compromise. A real sender may have been compromised, so the account should be investigated.
- **Email 03 and 08 passed authentication but still need checking.** A pass shows the email came from that domain's authorised servers. It doesn't show the request is genuine. A change of bank details, or a stranger asking for ID documents, needs verification through a known channel.
- **Email 13 uses a deceptive link.** In `shreeganesh-logistics[.]in[.]invoice-view-secure[.]com`, the real domain is `invoice-view-secure[.]com`. The familiar name is only a subdomain. Together with the macro-enabled file and the "enable editing" instruction, it is a typical malware-delivery pattern.

## Indicators of compromise

| Type | Indicator (defanged) | Email |
|---|---|---|
| Domain | solvex-industries-helpdesk[.]com | 02 |
| Domain | mail-secure-verify[.]net | 02 |
| Domain | verify-account-secure[.]com | 02 |
| Domain | gmail-corpmail[.]com | 05 |
| Domain | micros0ft-online[.]com | 07 |
| Domain | yandex-mailer[.]com | 10 |
| Domain | outlook-verify[.]info | 10 |
| Domain | lottery-verify[.]info | 10 |
| Domain | invoice-view-secure[.]com | 13 |
| Domain (Reply-To, to verify) | apexsteel-billing[.]com | 03 |
| Reply-To address | s.iyer.cfo.travel@outlook[.]com | 11 |
| IP address | 193.41.77.108 | 02 |
| IP address | 45.137.22.9 | 05 |
| IP address | 77.91.134.6 | 07 |
| IP address | 185.220.101.44 | 10 |
| IP address | 41.203.88.17 | 13 |
| Link | hxxp://solvex-industries-helpdesk[.]verify-account-secure[.]com/mailbox/confirm?user=aditya.rao | 02 |
| Link | hxxp://login[.]micros0ft-online[.]com/secure/verify-identity?ref=aditya.rao | 07 |
| Link | hxxp://claim-your-prize-now[.]lottery-verify[.]info/claim?ref=44921 | 10 |
| Link | hxxp://shreeganesh-logistics[.]in[.]invoice-view-secure[.]com/download?file=inv2207 | 13 |
| Attachment | JD_SeniorFinanceManager_Client.zip | 08 |
| Attachment | Pending_Invoice_Challan_Details.docm | 13 |

## Recommended actions

- **Suspicious emails (02, 05, 07, 10, 11, 13):** don't click, reply or pay. Report to the IT security team, block the domains and addresses above, and remove the emails. If anyone already acted, change passwords, enable multi-factor authentication and investigate for unauthorised access. For 05 and 11, verify through a known phone number or the official channel, and notify finance if money moved.
- **Medium risk (03, 08):** don't pay or send documents until the request is confirmed through contact details you already trust. Scan the ZIP before opening it.
- **Safe emails:** no action, but confirm the Drive file in Email 06 with the colleague if it was unexpected, and check the renewal amount in Email 09 against the records.

## What I would do differently

- Open links in a sandbox or a URL scanner, and check domain age with WHOIS. I judged links by their structure only.
- Analyse full raw headers, including the whole Received chain and DKIM and DMARC alignment, instead of a summary.
- Use a written scoring rubric so classifications are consistent. Emails 03, 06 and 08 sat on the borderline, and a rubric would make those decisions easier to explain.
- Automate the repetitive checks with a short Python script that reads `.eml` files and flags mismatched Reply-To or Return-Path addresses and failed authentication.
