# Git Troubleshooting Manual
Comprehensive Practical Guide for Daily Development

Last updated: 2026-02-20

---

# 📚 Table of Contents

1. Repository moved / renamed
2. Authentication failed (HTTPS / Token issues)
3. Permission denied (publickey)
4. Detached HEAD state
5. Non-fast-forward push rejected
6. Merge conflicts
7. Large file push failed
8. Accidental commit to wrong branch
9. Undo commits safely
10. Recover deleted branch
11. Clean Git cache / re-clone safely
12. Best Practices Checklist

---

# 1️⃣ Repository Moved / Renamed

### Error
```
remote: This repository moved.
```

### Fix
```bash
git remote set-url origin NEW_REPO_URL
git remote -v
git push
```

---

# 2️⃣ Authentication Failed (HTTPS)

### Error
```
remote: Support for password authentication was removed
```

### Fix (Use Personal Access Token)
1. Go to GitHub → Settings → Developer settings → Personal access tokens
2. Generate token (repo scope)
3. Use token as password

Optional: Cache credentials
```bash
git config --global credential.helper manager
```

---

# 3️⃣ Permission Denied (publickey)

### Error
```
Permission denied (publickey).
```

### Fix
Check SSH key:
```bash
ls ~/.ssh
```

If none exists:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Add public key to GitHub → SSH keys

Test:
```bash
ssh -T git@github.com
```

---

# 4️⃣ Detached HEAD

### Situation
You checked out a commit instead of a branch.

### Fix
Create branch:
```bash
git checkout -b new_branch_name
```

Or return:
```bash
git checkout main
```

---

# 5️⃣ Non-Fast-Forward Push Rejected

### Error
```
! [rejected] main -> main (non-fast-forward)
```

### Fix
```bash
git pull --rebase origin main
git push
```

If conflict occurs:
```bash
git rebase --continue
```

---

# 6️⃣ Merge Conflicts

Check status:
```bash
git status
```

Resolve conflict markers:
```
<<<<<<< HEAD
=======
>>>>>>> branch
```

Then:
```bash
git add .
git commit
```

---

# 7️⃣ Large File Push Failed

### Error
```
File exceeds GitHub's file size limit
```

### Fix (Use Git LFS)
```bash
git lfs install
git lfs track "*.bam"
git add .gitattributes
git commit -m "Track large files"
```

---

# 8️⃣ Committed to Wrong Branch

Move commit:
```bash
git checkout correct_branch
git cherry-pick COMMIT_HASH
```

Reset wrong branch:
```bash
git checkout wrong_branch
git reset --hard HEAD~1
```

---

# 9️⃣ Undo Commits Safely

Keep changes:
```bash
git reset --soft HEAD~1
```

Discard changes:
```bash
git reset --hard HEAD~1
```

Safe revert:
```bash
git revert COMMIT_HASH
```

---

# 🔟 Recover Deleted Branch

```bash
git reflog
git checkout -b recovered_branch HASH
```

---

# 1️⃣1️⃣ Clean Re-Clone Strategy

```bash
cd ..
rm -rf project_folder
git clone REPO_URL
```

---

# 1️⃣2️⃣ Best Practices Checklist

✅ Pull before push  
✅ Use branches  
✅ Avoid force push on shared main  
✅ Use git status frequently  
✅ Commit small logical changes  
✅ Clear commit messages  
✅ Proper .gitignore  

---

# 🧠 Advanced Commands

```bash
git log --oneline --graph --all
git remote -v
git branch -vv
```

---

# 🚀 Recommended Workflow

```bash
git pull
git checkout -b feature_x
git add .
git commit -m "Feature X"
git push -u origin feature_x
```

---

Most Git problems are reversible.
Use:

```bash
git status
git log
git reflog
```

End of Manual
