# Security Policy

This repository is part of a Amsterdam UMC research environment that handles potentially confidential data and code. To minimize risks of data leaks and protect research integrity, we follow strict security protocols throughout the Git development lifecycle.

---

## Scope

This policy applies to **GitHub-related threats only**, including:

- Accidental inclusion of confidential data (e.g., `.csv`, `.RData`, `.env`, `.xlsx`) in commits, pull requests, or issues.
- Unauthorized access to private repositories or GitHub Actions.
- Abuse of GitHub features such as Apps, Pages, or CI/CD pipelines.

Out of scope: Leaks via local runtime or SPE-contained environments (e.g., myDRE).

---

## Best Practices

### 1. Prevent Confidential Data Exposure

- Never commit files with the following extensions:

  - `.csv`, `.xlsx`, `.sav`, `.RData`, `.json`, `.env`, `.pem`, `.key`, `.pfx`

- Make sure all that these extensions are added to the `.gitignore` file
- Store data files in /data/ folder. Add `/data/` to `.gitignore`.
- Never hardcode paths to sensitive files — use environment variables instead
- Do not write secrets (tokens, keys, passwords) in code, comments, or documentation

### 2. Commit & Pull Request Hygiene

We recommend using [`pre-commit`](https://pre-commit.com/) to catch common issues **before commits are made**. This is a local tool that:

- Warns about large files (>100KB)
- Removes trailing whitespace
- Blocks commits with unresolved merge conflicts

> ⚠️ This tool is must be manually installed by each contributor.

**To enable it:**
```bash
pip install pre-commit
pre-commit install
```

It will then run automatically on each `git commit`.
See `.pre-commit-config.yaml` in this repository for configuration.

- Include a checklist in each pull request to confirm that:
  - [ ] No data or secrets are included
  - [ ] `.gitignore` is up to date

### 3. GitHub Actions & CI/CD

GitHub Actions CI is used to enforce security policy across all contributors. It includes:

- A workflow that blocks commits of high-risk file types (`.csv`, `.xlsx`, `.env`, etc.)
- Optional secret scanning or environment enforcement (via reusable workflows)

These checks run on:
- Every push to `main` or `master`
- Every pull request

❌ If a violation is detected, the workflow fails and the PR cannot be merged.

### 4. Repository Access

- Use 2FA on your GitHub account
- Restrict private repo access to verified collaborators only
- Review access regularly
- Do not make a repo public without a full data/code audit

---

## If a Leak Happens

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

## Reporting a Vulnerability

If you notice a vulnerability or accidental exposure:

- Do **not** open a public issue
- Contact the repository owner or institutional data officer privately
- Include the repo name, date, and general description of the issue
- Avoid including any actual sensitive content in your report

---

## References

- [GitHub Actions: Security best practices](https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions)
- [Trusted CI: Guide to Securing Scientific Software](https://trustedci.org/guide)
- [OWASP CIA + AAA Security Principles](https://owasp.org/www-project-cornucopia/)
