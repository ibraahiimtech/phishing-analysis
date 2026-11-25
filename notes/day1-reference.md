# Month 3.5 · Day 1 — How Email Works & Reading Headers

**Focus:** Why the visible email lies, how to read the header, and SPF/DKIM/DMARC —
plus the key nuance: passing the checks does NOT mean safe.

## Why this matters
Phishing is the #1 way attackers get in. A SOC analyst analyses suspicious emails
constantly, and "walk me through analysing a suspicious email" is a common interview
question.

## How email travels
An email hops through several mail servers (like sorting offices). Each stamps it
with a note. Those stamps pile up in the header — the hidden travel history.
The visible email can lie; the header shows where it really came from. "From" is
just a label the sender typed. The header reveals the real sending server.

## Header parts that matter
- From — who it CLAIMS to be (easy to fake — just a label)
- Return-Path / envelope sender — the REAL address used (mismatch = suspicious)
- Received — the server hops (newest at top); the real path + originating server
- Authentication-Results — the SPF/DKIM/DMARC verdicts (the gold)

## SPF / DKIM / DMARC (one line each)
- SPF — is this server ALLOWED to send for this domain? (IP vs approved list)
- DKIM — was the email TAMPERED with in transit? (a digital signature)
- DMARC — what to DO if SPF/DKIM fail? (reject / quarantine / allow)
Find Authentication-Results, read each as pass/fail. Any fail = red flag.

## THE KEY NUANCE (learned from a real example)
Passing SPF/DKIM/DMARC does NOT mean the email is safe. It only means the email
really came from the domain in the address. A scammer who OWNS their scam domain sets
up SPF/DKIM/DMARC correctly for it — so their phishing passes all three.
The checks answer "is it really from who the address says?" — NOT "is that sender
trustworthy?" Different questions.

## Hands-on done — real phishing email analysed
Example: "Landelijk Energieloket" (fake Dutch energy office).
- From: arkeero-nl2@mp.nl.znamost.com — display name looks official, but the real
  domain znamost.com is NOT an energy office. #1 tell: display name vs real address.
- SPF/DKIM/DMARC all PASSED — because the attacker owns znamost.com. Pass != safe.
- Body tells: fear + urgency ("prices rising", "offer ends this month"), unfilled
  placeholder "Beste {naam}," (mass template), a "check now" link, unsolicited.
- Verdict: phishing. Don't click. Delete/report.

## The analyst checklist for a suspicious email
Even if authentication PASSES, also check:
1. Does the real From address make sense for who it claims? (mismatch = bad)
2. Does the content use pressure / fear / urgency?
3. Were you expecting it?
Gut said "suspicious" despite the pass — and was right. Don't stop at "SPF passed."

## Key takeaways
1. The visible email lies; the header holds the truth (real path + verdicts).
2. SPF = allowed sender · DKIM = untampered · DMARC = what to do on failure.
3. Pass != safe — a scammer's own domain passes its own checks.
4. Always check: real From address, urgency/fear tactics, were you expecting it.

MITRE ATT&CK: T1566 (Phishing), T1566.002 (Spearphishing Link),
T1598 (Phishing for Information).
