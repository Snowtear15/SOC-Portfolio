# Writeups template

# [Alert/Case Name] — [Platform] ([Alert type, e.g. Phishing Triage])

> **TL;DR:** [2 lines max: what the alert was, your verdict, the one key piece of evidence. Recruiters skim — this is sometimes all they read.]

**Date:** YYYY-MM-DD · **Platform:** [THM SOC Simulator / LetsDefend / BTLO / Home Lab] · **Tools:** [Splunk, etc.]

***

## Scenario

[2–4 sentences. What alert fired, what it claimed, what the environment was. Written so a non-participant understands the starting point. Paraphrase — never paste the alert text wholesale.]

## Investigation

[10–20 lines. Chronological, each step = what question I was answering → what I searched/looked at → what I found. Include:]

* The actual queries/searches you ran (in code blocks — recruiters and interviewers love seeing real SPL/KQL)
* Key evidence found, with specific values (timestamps, IPs, domains)
* 1–3 screenshots MAX, only ones showing evidence (a log entry, a query result) — never UI tours
* Your reasoning at pivot points: "email claimed X, so I checked Y to verify"

```
[example: the Splunk search you ran]
```

## Verdict

**Classification:** True Positive / False Positive **Escalated:** Yes/No
[2–4 sentences: verdict + the evidence chain that justifies it. If relevant, map to MITRE: e.g. T1566.002 (Phishing: Spearphishing Link).]

## Response Actions

[Bulleted, executable actions — the checklist an L2/IR team could run:]

* [containment: resets, session revokes, blocks]
* [scoping: search for other victims/recipients]
* [cleanup: purge, scan]

## IOCs

| Type | Value (defanged) | Source |
| ---- | ---------------- | ------ |
| Domain | example[.]co | Firewall log (observed) |
| URL | hxxps://... | Email body |
| IP | x.x.x.x | Firewall log (observed) |

## What I Learned

[2–3 lines, honest and specific. "Learned to distinguish observed vs claimed IOCs" beats "learned about phishing." This section is disproportionately what makes writeups feel human and credible — don't skip it.]