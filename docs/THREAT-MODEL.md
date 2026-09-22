# Threat Model

## Assets

- source code
- build environment
- GitHub repository
- authentication data
- local configuration
- downloaded files
- user privacy
- system integrity

## Trust boundaries

### T1 — Source code

Question: what does the application itself implement?

### T2 — Backend/API

Question: what remote services does the application contact and why?

### T3 — Community source configuration

Question: what data does a configured source provide to Hydra?

### T4 — Download infrastructure

Question: where does a selected download actually originate?

### T5 — Downloaded software

Question: what does the downloaded file do when executed?

## Threat categories

- credential exposure
- malicious or compromised dependencies
- unexpected network activity
- unexpected persistence
- unexpected filesystem modification
- supply-chain compromise
- malicious third-party content
- accidental publication of private research data

## Analysis rule

Evidence must be tied to the correct trust boundary. Do not collapse T3, T4 and T5 into conclusions about T1 without evidence.
