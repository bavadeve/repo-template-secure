# Security Policy

This repository is part of a research environment that handles potentially confidential data and code. To minimize risks of data leaks and protect research integrity, we follow strict security protocols throughout the Git development lifecycle.

---

## 🧭 Scope

This policy applies to **GitHub-related threats only**, including:
- Accidental inclusion of confidential data (e.g., `.csv`, `.RData`, `.env`, `.xlsx`) in commits, pull requests, or issues.
- Unauthorized access to private repositories or GitHub Actions.
- Abuse of GitHub features such as Apps, Pages, or CI/CD pipelines.

Out of scope: Leaks via local runtime or SPE-contained environments (e.g., myDRE).

---

## 🔐 Best Practices

### 1. 🔥 Prevent Confidential Data Exposure

- Never commit files with the following extensions:
  - `.csv`, `.xlsx`, `.sav`, `.RData`, `.json`, `.env`, `.pem`, `.key`, `.pfx`
- Add all of the above to `.gitignore`
- Store data files outside the Git repository folder
- Never hardcode paths to sensitive files — use environment variables instead
- Do not write secrets (tokens, keys, passwords) in code, comments, or documentation

### 2. ✅ Commit & Pull Request Hygiene

- Use [pre-commit hooks](https://pre-commit.com/) to block sensitive content
- Run `gitleaks` or similar scanners before pushing code
- Include a checklist in each pull request to confirm that:
  - [ ] No data or secrets are included
  - [ ] `.gitignore` is up to date

### 3. 🤖 GitHub Actions & CI/CD

- Only use vetted and trusted GitHub Actions
- Define explicit permissions in workflows (`permissions:` block)
- Use GitHub Encrypted Secrets (never hardcoded credentials)
- Monitor CI logs for unintentional exposure

### 4. 🔒 Repository Access

- Use 2FA on your GitHub account
- Restrict private repo access to verified collaborators only
- Review access regularly
- Do not make a repo public without a full data/code audit

---

## 🔁 If a Leak Happens

1. **Public Repo**:
   - Immediately set the repo to private or take it offline
   - Contact the privacy officer or project lead
   - Scrub history using [`git filter-repo`](https://github.com/newren/git-filter-repo) or [`BFG`](https://rtyley.github.io/bfg-repo-cleaner/)
   - Notify any collaborators or affected parties

2. **Private Repo**:
   - Audit access logs
   - Review push/clone/download events
   - Proceed with full data removal as above

---

## 🧪 CODECHECK & Reproducibility Notes

- Use `renv::snapshot()` (R) or `requirements.txt` (Python) to track package environments
- Prefer Quarto/R Markdown for reproducible reports — minimizes copy-paste
- Maintain `sessionInfo()` or equivalent for reproducibility audits
- Clearly document any proprietary code or secure data locations in the `README`

---

## 🧾 Example `.gitignore`

```gitignore
# Prevent accidental commit of sensitive files
*.csv
*.xlsx
*.sav
*.RData
*.json
*.env
*.pem
*.key
*.pfx
*.sqlite
/data/
