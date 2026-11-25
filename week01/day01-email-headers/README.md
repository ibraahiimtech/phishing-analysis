# Day 01 — Email Headers & SPF/DKIM/DMARC (analysis, no local tools)

Analysed a real phishing email's header by hand. No scripts — the artifact is the
analysis itself.

What was done:
- Learned how email travels and why the header holds the truth (not the "From" line)
- SPF / DKIM / DMARC — what each checks (allowed sender / untampered / what to do on fail)
- Analysed a real phishing email ("Landelijk Energieloket", from znamost.com):
  passed SPF/DKIM/DMARC but was still phishing — because the attacker owns the domain
- KEY lesson: authentication "pass" != safe; also check the real From address,
  urgency/fear tactics, and whether you expected the email

Learning artifact: notes/day1-reference.md
