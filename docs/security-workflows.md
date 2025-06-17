# 🔐 How This Project Helps Protect Your Data

This project includes automated checks and setup files that help reduce the risk of accidentally uploading sensitive data to GitHub.

These checks are not perfect — but together, they catch most common mistakes before they cause problems.

---

## 1. GitHub Actions: Automatic Checks (After Upload)

Each time you upload changes to GitHub (a “push” or pull request), GitHub will run an automated check.

✅ If everything looks okay, your changes are accepted.
❌ If you accidentally added a file with a sensitive extension (like `.csv` or `.env`), the check will fail, and GitHub will show a red ❌ with a message.

> ⚠️ Important: This check runs **after** your code is already uploaded. It does **not prevent** you from uploading files — it just notifies you if something went wrong.

That’s why we recommend keeping repositories **private by default**, and only making them public if you're confident the data is clean. See [docs/public-release.md](public-release.md) for more.

---

## 2. `.gitignore`: Prevent Files from Being Tracked

This project includes a `.gitignore` file that tells Git:

> “Don’t track or upload any files with these extensions.”

This includes file types like:
- `.csv`
- `.xlsx`
- `.RData`
- `.env` (files with passwords or API keys)

If you try to add one of these files with a normal `git add`, Git will ignore it silently.

---

## 3. Optional: Pre-Commit Hooks (Before Upload)

If you want an extra safety net **before** files are ever uploaded to GitHub, you can install something called `pre-commit`.

It runs automatic checks every time you try to commit something locally — like a spellcheck or safety check for your code and files.

This template includes a ready-to-use `.pre-commit-config.yaml` that:

✅ Blocks files larger than 100KB
✅ Warns you about unresolved merge conflicts
✅ Cleans up things like extra spaces or missing newlines

### 🧪 How to enable it (once per computer)

1. Install `pre-commit`:

   ```bash
   pip install pre-commit
   ```

2. Enable it in your project folder:

   ```bash
   pre-commit install
   ```

After that, `pre-commit` will run every time you commit something. You can always disable or adjust it later.

---

## Summary: Three Layers of Safety

| Tool              | When it runs     | What it catches                                 |
|-------------------|------------------|--------------------------------------------------|
| `.gitignore`      | Before `git add` | Prevents tracking sensitive file types          |
| `pre-commit`      | Before `git commit` | Warns about large files, formatting, mistakes |
| GitHub Actions CI | After `git push` | Blocks changes that include forbidden files     |

No single step is perfect — but together, they make mistakes much less likely.
If you ever have doubts, ask your project lead or data steward before pushing your code.
