# How to Fix a GitHub Repository That Has Been Moved (Repository Renamed)

Last updated: 2026-02-20

---

## 🔎 Situation

When pushing to GitHub, you see a message like:

```
remote: This repository moved. Please use the new location:
remote:   https://github.com/USERNAME/NEW_REPO_NAME.git
To https://github.com/USERNAME/OLD_REPO_NAME.git
   24796b4..18ced38  HEAD -> main
```

### What This Means

- The repository has been **renamed or transferred**
- GitHub is currently redirecting traffic from the old repository name to the new one
- Your push succeeded, but your local Git remote still points to the **old URL**

It is recommended to update your local remote to avoid future issues.

---

# ✅ Step-by-Step Fix

---

## Step 1️⃣ Check Current Remote

Open Git Bash (or terminal) and run:

```bash
git remote -v
```

You may see something like:

```
origin  https://github.com/USERNAME/OLD_REPO_NAME.git (fetch)
origin  https://github.com/USERNAME/OLD_REPO_NAME.git (push)
```

This confirms your local repo still points to the old location.

---

## Step 2️⃣ Update Remote URL

Run:

```bash
git remote set-url origin https://github.com/USERNAME/NEW_REPO_NAME.git
```

Replace:
- `USERNAME` with your GitHub username
- `NEW_REPO_NAME` with the new repository name

---

## Step 3️⃣ Verify It Was Updated

Run again:

```bash
git remote -v
```

Now it should show:

```
origin  https://github.com/USERNAME/NEW_REPO_NAME.git (fetch)
origin  https://github.com/USERNAME/NEW_REPO_NAME.git (push)
```

---

## Step 4️⃣ Test Push

```bash
git push
```

You should no longer see the "repository moved" message.

---

# 🧠 Why This Happens

This usually occurs when:

- You renamed the repository on GitHub
- You transferred it to another account or organization
- You recreated it with a new name

GitHub provides automatic redirect, but it's best practice to update your remote.

---

# 🔁 Optional: If You Want to Re-add Remote (Alternative Method)

If something goes wrong, you can remove and re-add origin:

```bash
git remote remove origin
git remote add origin https://github.com/USERNAME/NEW_REPO_NAME.git
```

Then push:

```bash
git push -u origin main
```

---

# 🎯 Summary

| Action | Command |
|--------|----------|
| Check remote | `git remote -v` |
| Update remote | `git remote set-url origin NEW_URL` |
| Verify | `git remote -v` |
| Push | `git push` |

---

# 📌 Best Practice

After renaming a GitHub repository, always:

1. Update your local remote URL
2. Test with `git push`
3. Confirm no redirect warning appears

---

End of tutorial.
