# Contributing to VaultRAG Lite

Thanks for your interest! VaultRAG Lite is the free, MIT-licensed core of the VaultRAG project. Contributions that make it **simpler, safer, more reliable, or easier to run** are very welcome.

## What belongs in Lite (and what doesn't)

Lite has a deliberately small scope: upload `.txt` / `.md` / `.pdf`, embed locally, ask questions, get answers from a local LLM.

| Great PRs | Likely to be declined |
|---|---|
| Bug fixes, crash fixes, clearer error messages | Features that are part of the paid **Enterprise** edition (auth, citation validation, DOCX/CSV, per-document erasure, audit logging, ...) |
| Documentation, typos, translations | Anything that sends data to a third party or adds telemetry |
| Test coverage, CI, type hints | Large new dependencies for marginal gain |
| Performance and memory improvements | Cloud LLM / API integrations (the project is local-only by design) |
| Compatibility fixes (new Ollama / Chroma versions, Windows / macOS / ARM) | Framework rewrites |

Not sure? Open a **Discussion** or an issue first - it saves everyone time.

## Ground rules

1. **Local-first is non-negotiable.** No outbound network calls other than to the user's own Ollama instance. No analytics, no "phone home", no auto-update checks.
2. **Never commit private data** - no real documents, `.env` files, API keys, or model files. Use synthetic sample text in tests and screenshots.
3. **Be kind.** We follow the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/) v2.1. Report unacceptable behaviour to `conduct@YOUR_DOMAIN.com`.
4. **Security issues are not public issues.** See [SECURITY.md](SECURITY.md).

## Development setup

Requirements: Python 3.11+, [Ollama](https://ollama.com) running locally, and ~8 GB of free RAM for a 7B model.

```bash
git clone https://github.com/YOUR_ORG/vaultrag.git
cd vaultrag/src_lite

python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt

ollama pull qwen2.5:7b
ollama pull nomic-embed-text

uvicorn main:app --reload          # terminal 1 -> http://localhost:8000/docs
streamlit run app.py               # terminal 2 -> http://localhost:8501
```

Or with Docker:

```bash
cd src_lite
docker compose up -d --build
```

## Code style

- Python 3.11+, type hints on all function signatures, `from __future__ import annotations`.
- Keep functions short and single-purpose. Prefer the standard library over a new dependency.
- Format with `ruff format` and lint with `ruff check` (line length 120).
- Comments explain *why*, not *what*.
- Pin new dependencies to exact versions in `requirements.txt`.

## Pull request process

1. Fork the repo and create a branch: `git checkout -b fix/short-description`.
2. Make focused commits. We prefer [Conventional Commits](https://www.conventionalcommits.org/) (`fix:`, `feat:`, `docs:`, `chore:`).
3. Test your change end to end (upload a file, ask a question, check the logs).
4. Fill in the pull request template completely.
5. A maintainer will review, usually within a few days. Please be patient - this is a small team.

By submitting a pull request you agree that your contribution is licensed under the project's [MIT License](LICENSE).

## Reporting bugs

Open an issue with:

- What you expected vs. what happened
- Steps to reproduce (with a **synthetic** document, never a confidential one)
- Versions: OS, Python, Docker, Ollama, model names
- Relevant logs (`docker compose logs backend`) with secrets removed

## Need something Lite doesn't do?

That's what **VaultRAG Enterprise** is for - the full production stack with auth, validated citations, more file formats, and erasure endpoints. See the comparison in the [README](README.md).
