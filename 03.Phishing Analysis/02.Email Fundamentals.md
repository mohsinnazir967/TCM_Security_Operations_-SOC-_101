## Email Fundamentals

**Goal**: Understand how email works—essential for email header analysis, sender attribution, and phishing investigations.

---

### How Email Works (SMTP Overview)

- Emails are sent using **SMTP (Simple Mail Transfer Protocol)**.
- SMTP servers act like post offices: transferring messages between clients and recipient servers.
- Common SMTP ports:
  - `25` (default)
  - `465` (SMTPS)
  - `587` (SMTP with TLS)

####  Example Flow:
1. Bob (Gmail) sends email to Alice (Yahoo).
2. Bob's email client → connects to Gmail's SMTP server.
3. SMTP authenticates sender (username/password).
4. Gmail SMTP looks up Yahoo's SMTP via **DNS MX records**.
5. Message is routed → Yahoo’s SMTP server.
6. Alice logs in → retrieves email using **POP3 or IMAP**.

---

### Key Email Components

#### Email Headers
- Contain **metadata**: sender, receiver, subject, timestamps, routing info.
- **Important for analysis**: Can help trace source, detect spoofing, view relays.
- Many headers are **hidden by default** in clients (e.g., Thunderbird, Outlook).
- **Attackers can spoof headers**, so don’t trust them blindly.
- Headers include:
  - `From`, `To`, `Reply-To`
  - `Date`, `Subject`
  - `Received`, `Message-ID`, `Return-Path`
- Full headers can be exported for analysis.

####  Email Body
- Main content area: can contain **text, HTML, CSS, links, images**.
- Rendered like a web page in most clients.
- Raw content (HTML source) view reveals code & embedded resources.

---

###  Email Address Structure

- Format: `username@domain.com`
- Components:
  - **Local Part** (e.g., `bob.smith`)
    - User or mailbox identifier
    - May include dots, hyphens, underscores
  - **Domain Part** (e.g., `example.com`)
    - Mail server domain
    - Includes TLD like `.com`, `.org`, `.co.uk`

- DNS **MX (Mail Exchange)** records resolve domain to mail server IP.

---

###  Common Email Protocols

| Protocol | Purpose | Port | Notes |
|---------|---------|------|-------|
| **SMTP** | Sends outgoing email | 25 | Also uses 465/587 with encryption |
| **POP3** | Downloads & deletes emails | 110 | POP3S uses 995 (SSL) |
| **IMAP** | Syncs email across devices | 143 | IMAPS uses 993 (TLS) |

- **POP3**: One device only; downloads + deletes emails.
- **IMAP**: Syncs across devices; emails stay on server.

---

###  Email Infrastructure Components

- **MTA (Mail Transfer Agent)**:
  - Routes emails between mail servers (relay chain).
  - Adds **"Received" headers** at each hop (key for tracing source).
- **MUA (Mail User Agent)**:
  - Interface used by users (e.g., Gmail, Outlook).
  - Sends email to MTA, retrieves using POP3/IMAP.
- **MDA (Mail Delivery Agent)**:
  - Delivers received email to the correct user mailbox.
  - Applies filters, sorts folders.

>  Optional terms (less commonly discussed):
> - **MSA** (Mail Submission Agent) → overlaps with MUA.
> - **MRA** (Mail Retrieval Agent) → overlaps with MDA.

---

### Summary

- Email delivery = multi-stage process: MUA → MTA(s) → MDA.
- Protocols (SMTP, POP3, IMAP) govern sending and receiving.
- Headers & routing info are essential for phishing analysis.
- Understanding infrastructure helps trace spoofing, manipulation, and identify malicious senders.

---
