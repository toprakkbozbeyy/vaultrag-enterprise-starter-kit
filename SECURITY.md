# Security Policy

VaultRAG exists to keep sensitive documents inside your own infrastructure. We take vulnerabilities in it seriously and appreciate responsible disclosure.

## Supported versions

| Version | Edition | Security fixes |
|---|---|---|
| `main` / latest release | Lite (MIT) | Yes |
| Older Lite releases | Lite (MIT) | Best effort - please upgrade |
| Latest Enterprise release | Enterprise | Yes - delivered to customers through Whop |

## Reporting a vulnerability

**Please do not open a public GitHub issue for security problems.**

Use one of these private channels:

1. **GitHub Private Vulnerability Reporting** - go to the repository's **Security** tab -> **Report a vulnerability** (preferred).
2. **Email:** `security@YOUR_DOMAIN.com`
   Use the subject line `VaultRAG security report`. If you need to send sensitive proof-of-concept material, ask for a PGP key first.

Please include:

- A description of the issue and its impact
- Steps to reproduce, or a minimal proof of concept (use synthetic data only)
- Affected version / commit and your environment (OS, Docker, Ollama and model versions)
- Any suggested fix, if you have one

## What to expect

| Step | Target time |
|---|---|
| Acknowledgement of your report | within 3 business days |
| Initial assessment and severity rating | within 7 days |
| Fix or mitigation plan | within 30 days for high/critical issues |
| Public advisory and credit (if you wish) | after a fix is available |

These are good-faith targets from a small team, not contractual SLAs. Enterprise customers with a support agreement receive priority handling through their private channel.

## Scope

**In scope**

- Authentication / authorization bypass (Enterprise API-key handling)
- Path traversal, arbitrary file read/write via upload handling
- Remote code execution, deserialization or injection flaws in the API or UI
- Any code path that sends user documents, queries, or metadata to a third party (a violation of the zero-egress design)
- Prompt-injection issues that let document content cause actions beyond answering text
- Insecure defaults in the provided Docker / Compose files (for example, unintentionally exposed ports)
- Vulnerable pinned dependencies with a realistic exploit path

**Out of scope**

- Vulnerabilities in Ollama, ChromaDB, Streamlit, Docker or the underlying OS themselves - please report those upstream (we do want to hear about it if our pinned version is affected)
- Findings that require physical access, or a compromised host / administrator account
- Denial of service through unrealistically large inputs on hardware you control
- Missing security headers or hardening on deployments where the operator deliberately exposed the service without TLS or authentication
- Social engineering, spam, or reports from automated scanners without a demonstrated impact
- LLM output quality, hallucinations or model jailbreaks that do not cross a security boundary

## Safe harbor

If you act in good faith - test only against your own installation, avoid privacy violations and data destruction, and give us reasonable time to respond before disclosure - we will not pursue legal action against you and will work with you to resolve the issue.

## Our security design (for reviewers)

- **Zero egress at runtime:** documents, questions, embeddings and answers are processed by local components only. The only outbound traffic is the one-time model download.
- **No telemetry:** ChromaDB anonymized telemetry is disabled; Streamlit usage statistics are disabled.
- **Least exposure by default:** Compose publishes the UI and API on `127.0.0.1` only; Ollama is never published.
- **Non-root containers:** application containers run as an unprivileged user.
- **Bounded input:** upload size limits and an allow-list of file types.

## Your responsibilities as an operator

VaultRAG is a building block, not a certified product. You remain responsible for TLS termination, disk encryption, network segmentation, user authentication, backups, retention policy, and your own legal and compliance assessment (GDPR, HIPAA, or other frameworks).

Thank you for helping keep VaultRAG and its users safe.
