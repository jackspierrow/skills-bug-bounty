---
name: agentic-bug-hunter
description: Agentic bug bounty hunting workflow (recon → learn → hunt → validate → report) adapted from AwareXone's Agentic-Bug-Hunter — 7-Question Gate, A→B→C bug chaining, 26 web2 vuln classes, 10 smart-contract bug classes with Foundry PoC, report templates for HackerOne/Bugcrowd/Intigriti/Immunefi. Use for ANY bug bounty task for pradana: starting a new target, doing recon, auditing source code or smart contracts, validating a finding, or writing a submission-ready report. Trigger on "cari bug", "hunt bug", "gas bug", bug bounty program names, or "tambahin skill bug".
metadata:
  author: "AwareXone (adapted for pradana)"
  source: "https://github.com/awarexone/Agentic-Bug-Hunter"
  local_copy: "~/workspace/agentic-bug-hunter/"
  version: "1.0.0"
  license: MIT
---

# Agentic Bug Hunter (for pradana)

Full pipeline: **Recon → Learn → Hunt → Validate → Report**. Deep playbooks live in the local repo copy at `~/workspace/agentic-bug-hunter/skills/` — read the matching one before hunting:

- `skills/bug-bounty/SKILL.md` — master workflow (all vuln classes, chains, report)
- `skills/bb-methodology/SKILL.md` — hunting mindset, 5-phase workflow, session discipline
- `skills/web2-recon/SKILL.md` — subdomain enum, live hosts, URL crawl, nuclei
- `skills/web2-vuln-classes/SKILL.md` — 21 bug classes + bypass tables
- `skills/security-arsenal/SKILL.md` — payloads, bypass tables, gf patterns
- `skills/triage-validation/SKILL.md` — 7-Question Gate, 4 gates, never-submit list
- `skills/report-writing/SKILL.md` — H1/Bugcrowd/Intigriti/Immunefi templates, CVSS 3.1
- `skills/web3-audit/SKILL.md` — smart contract audit, 10 bug classes, Foundry PoC template
- `skills/graphql-audit/SKILL.md`, `skills/cloud-pentest/SKILL.md`, `skills/cicd-security/SKILL.md`, `skills/mobile-pentest/SKILL.md`, `skills/mcp-server-audit/SKILL.md` — specialty hunts

## THE ONLY QUESTION THAT MATTERS

> "Can an attacker do this RIGHT NOW against a real user who took NO unusual actions — and does it cause real harm (stolen money, leaked PII, account takeover, code execution)?"

If NO — STOP. Do not write. Do not explore further. Move on. Theoretical bugs are wasted time.

## Rules (always on)

1. **Read full scope first** — only test what the program authorizes. One out-of-scope request can get the account banned.
2. **Real bugs only** — prove it works or drop it. "Could" is not a bug.
3. **Kill weak findings fast** — run the 7-Question Gate BEFORE writing any report.
4. **Impact first** — hunt the worst consequence first (funds, PII, ATO, RCE).
5. **5-minute rule** — no progress after 5 min probing? Move on. **One-hour rule** — stuck an hour with nothing? Switch context.
6. **One bug class at a time** — go deep, don't spray.
7. **Hunt less-saturated classes** — XSS/SSRF have the most competition. Prefer business logic, race conditions, OAuth/OIDC chains, cache poisoning, CI/CD, GraphQL.

## The 7-Question Gate (all 7 must be YES before writing a report)

1. Can I exploit this RIGHT NOW with a real PoC (exact request)?
2. Does it affect a REAL user who took NO unusual actions?
3. Is the impact concrete (money, PII, ATO, RCE)?
4. Is this in scope per the program policy?
5. Did I check Hacktivity/changelog/audit reports for duplicates?
6. Is this NOT on the always-rejected list (headers alone, introspection alone, self-XSS, open redirect alone, DNS-only SSRF, etc.)?
7. Would a tired triager at 5pm Friday say "yes, that's a real bug"?

## A→B→C Bug Chains (chains pay 3–10x more)

When bug A is confirmed, hunt B and C nearby: IDOR read → PUT/DELETE same endpoint; SSRF → cloud metadata 169.254.169.254 → IAM creds → RCE; stored XSS → HttpOnly missing → session hijack → ATO; open redirect → OAuth redirect_uri → code theft → ATO; S3 listing → JS bundles → OAuth secret → OAuth chain. One report per chain, not per bug.

## Web3 — 10 Smart Contract Bug Classes

Accounting desync, access control, incomplete code path, off-by-one, oracle manipulation, ERC4626 share inflation, reentrancy, flash loan attack, signature replay, proxy/upgrade. Typical payouts $10K–$2M. Use Foundry PoC template from `skills/web3-audit/`. Rust lesson: only panics on deserialization/decoding of network input are exploitable; `.unwrap()` on encoding paths is not.

## Report (keep < 600 words, human tone)

Title formula: `[Bug Class] in [Exact Endpoint/Feature] allows [attacker] to [impact]`. First sentence states exact impact in plain English. Steps to reproduce = copy-pasteable request + response showing the bug. CVSS 3.1 included. One concrete example beats three abstract sentences. No em dashes, no "comprehensive/leverage/seamless".

## Pradana guardrails (standing, override nothing below)

- **FREE ONLY + ATURAN FEE 100x (user 2026-11-12 ~14:26 WIB).** Never pay a submission fee, stake, or burn without his explicit approval after seeing the amount. AND: before calling ANY submission "paid" and refusing to submit, verify the fee 100x from primary sources (live submission form + program docs + independent source) — never reject a submit on an unverified fee claim. Cantina is FREE (the old "$50" note was WRONG — Sherlock charges $250 USDC/report). Fees claimed before (verify each before blocking): Immunefi, Hastra $10, Firedancer 1 SOL, Sui $20, Lombard, TrustSwiftly $500, Ethereum Foundation $10 ETH burn, Aave V4 250 USDC stake. Report fee gates; hunt first, submit only with a yes.
- **Never create platform accounts silently** (no Bugcrowd/Intigriti/YesWeHack/Cantina/HackerOne account without his go-ahead). He has HackerOne `kazekagemadara` (2 trial slots left — don't burn them on weak findings) and HackenProof `@jhontheripper160` rep 0.
- **One report per program at a time.** Dedup against the actual submission venue, not just the code repo (XE-3 lesson).
- **Never submit public issues** when a program forbids it.
- **After a VERIFIED send:** record it in `~/workspace/shelleymaeph-bug-bounties/draft-siap-submit.md` with the read-back Gmail ID, email a reminder to zorindellvierow@gmail.com (the other agent), and track the payout — check payout status periodically so a win is never missed. Bug-bounty sends go ONLY through the hourly bounty cron, never the Gmail worker.
- **"JAHAT" rule:** report EVERY verified finding however small, method legitimate/in-scope.
- **"GUNAIN AKAL":** rotate email submissions across his Gmails, different reports per HackerOne account, X throwaways monitor announcements, Wayback-JWT + Google Dorks, GitHub PVR.
