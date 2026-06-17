# VaultGuard — Privileged Access Management

A browser-based Privileged Access Management (PAM) simulation built as a hands-on IAM portfolio project. No backend. No frameworks. Pure HTML, CSS, and JavaScript with localStorage persistence.

**Live Demo:** [PAM.mmohamud.me](https://PAM.mmohamud.me)

---

## What It Does

This project simulates a real-world PAM environment where privileged credentials are never owned, only checked out. Every privileged session is time-bound, approved, recorded, and auditable, mirroring how enterprise tools like CyberArk and BeyondTrust manage standing access risk.

### Features

| Module | Description |
|---|---|
| Dashboard | Live stats: vaulted accounts, checked-out credentials, pending requests, high-risk sessions |
| Credential Vault | Privileged accounts stored centrally, tiered by risk (root, domain admin, DB admin, network, service) |
| Access Requests | Just-In-Time access requests with justification and time-bound duration |
| Approval Workflow | Requests sit pending until approved or denied; approval instantly checks out the account |
| Active Sessions | Live countdown timer per session, calculated risk score, and a one-click kill switch |
| Session Replay | Command-by-command recording of every session with high-risk commands flagged |
| Audit Trail | Immutable, timestamped log of every vault, request, and session event |

---

## PAM Concepts Demonstrated

- **No Standing Privilege** — credentials are checked out for a defined window, never permanently assigned
- **Just-In-Time (JIT) Access** — access is time-bound and automatically expires when the session timer hits zero
- **Approval Workflow** — no privileged session begins without explicit approval
- **Session Recording** — every command run during a privileged session is logged for accountability
- **Risk Scoring** — sessions are scored based on account tier and the presence of high-risk commands
- **Kill Switch** — any active session can be terminated instantly, revoking access in real time
- **Immutable Audit Trail** — every vault, request, and session action is permanently logged

---

## How Session Risk is Calculated

```
Risk Score = Base Tier Risk + (15 × number of high-risk commands run)

Tier Base Risk:
  Root / Superuser     → 40
  Domain Admin         → 35
  Database Admin       → 25
  Network Admin        → 25
  Service Account      → 10
```

High-risk commands (e.g. password resets, shadow file access, production config changes) are flagged inline in the session replay so reviewers can immediately spot what mattered in a session instead of reading the full transcript.

---

## Default Data

The system seeds with five vaulted accounts across different privilege tiers and one completed sample session so the Session Replay view is never empty on first load:

**Vaulted Accounts:** `prod-db-admin` (PostgreSQL Production), `root-webserver-01` (Ubuntu Web Server), `da-corp` (Active Directory), `core-switch-admin` (Cisco Core Switch), `cicd-deploy-svc` (Kubernetes Cluster).

---

## Tech Stack

- Vanilla HTML, CSS, JavaScript
- localStorage for data persistence (no backend required)
- Google Fonts: Playfair Display, DM Sans, JetBrains Mono
- Deployed via GitHub Pages with a custom subdomain

---

## How to Run Locally

```bash
git clone https://github.com/mmohamud25/pam-system.git
cd pam-system
open index.html
```

No install. No build step. Open the file and it works.

---

## Deploying to GitHub Pages

1. Push `index.html` and `CNAME` to your repo's `main` branch
2. Go to **Settings > Pages**
3. Set source to `main` branch, root folder
4. In your DNS provider, add a `CNAME` record pointing `PAM` to `mmohamud25.github.io`
5. Confirm the custom domain in GitHub Pages settings and enable HTTPS

The included `CNAME` file already points to `PAM.mmohamud.me`.

---

## Project Context

This is part of a broader IAM and security architecture portfolio built to demonstrate hands-on knowledge of access control models, alongside certifications including CompTIA Security+ (SY0-701) and ISC2 Certified in Cybersecurity (CC).

**Related projects:**
- [RBAC System](https://rbac-system.mmohamud.me) — Role-Based Access Control with identity lifecycle management
- [ZeroGuard](https://zerotrust.mmohamud.me) — Zero Trust access model with a dynamic trust scoring and policy engine

**Planned follow-up projects:**
- Identity Governance Dashboard (access request and approval workflows)
- OAuth 2.0 / OIDC SSO Demo

---

## Author

**Mohamed Mohamud**
Founder, Kulan Group | Cybersecurity & Technology
[mmohamud.me](https://mmohamud.me) · [linkedin.com/in/mohamed-2-mohamud](https://linkedin.com/in/mohamed-2-mohamud)
