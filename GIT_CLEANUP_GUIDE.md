# Git Repository Cleanup Guide

## Problem

The `.env` and `.env.production` files were accidentally committed to GitHub with sensitive credentials.

## Solution

Follow these steps to remove them from Git history:

### Step 1: Remove Files from Git (Keep Locally)

```bash
cd AIP_UI

# Remove from Git tracking but keep local files
git rm --cached .env
git rm --cached .env.production

# Commit the removal
git commit -m "Remove sensitive env files from tracking"
```

### Step 2: Verify .gitignore is Correct

Your `.gitignore` now has:

```gitignore
# Environment files (never commit credentials!)
.env
.env.local
.env.development.local
.env.test.local
.env.production
.env.production.local
!.env.example
```

This ensures:
- `.env` is ignored
- `.env.production` is ignored  
- `.env.example` is allowed (it's a template, no credentials)

### Step 3: Add .env.example to Git

```bash
# This is safe - it's just a template with no credentials
git add .env.example
git add .gitignore
git commit -m "Add .env.example template and update .gitignore"
```

### Step 4: Push Changes

```bash
git push
```

### Step 5: Remove from Git History (Optional but Recommended)

If the env files contained real credentials, you should remove them from Git history:

**Option A: Using git filter-branch**
```bash
# Remove .env from all commits
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch .env .env.production" \
  --prune-empty --tag-name-filter cat -- --all

# Force push (WARNING: This rewrites history)
git push --force --all
```

**Option B: Using BFG Repo-Cleaner (Easier)**
```bash
# Install BFG
# Download from: https://rtyley.github.io/bfg-repo-cleaner/

# Remove files
bfg --delete-files .env
bfg --delete-files .env.production

# Clean up
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# Force push
git push --force --all
```

### Step 6: Rotate Credentials

**IMPORTANT:** If your `.env` or `.env.production` contained real credentials:

- [ ] Change database passwords
- [ ] Rotate API keys
- [ ] Update JWT secrets
- [ ] Regenerate any tokens
- [ ] Update credentials on hosting platform

### What Should Be in Git

**YES - Commit these:**
- `.env.example` (template with no real credentials)
- `.gitignore`
- All source code
- Configuration files (without secrets)

**NO - Never commit these:**
- `.env` (contains real credentials)
- `.env.production` (contains production credentials)
- `.env.local`
- Any file with real API keys, passwords, or secrets

### Verification

After cleanup, verify:

```bash
# Check what's tracked
git ls-files | grep env

# Should only show:
# .env.example
# (NOT .env or .env.production)
```

### Going Forward

1. **Before committing**, always check:
   ```bash
   git status
   ```

2. **Look for**:
   - Files with `.env` (except `.env.example`)
   - Files with credentials
   - Database dumps
   - API keys

3. **Use git add selectively**:
   ```bash
   # Good - specific files
   git add src/
   git add .gitignore
   git add .env.example
   
   # Bad - adds everything (including secrets)
   git add .
   ```

## Quick Fix Commands

Run these now:

```bash
cd AIP_UI

# 1. Remove from tracking (keeps local files)
git rm --cached .env
git rm --cached .env.production

# 2. Stage the changes
git add .gitignore
git add .env.example

# 3. Commit
git commit -m "Remove sensitive env files and add .env.example template"

# 4. Push
git push
```

## Summary

- `.gitignore` is now fixed
- `.env` and `.env.production` will be ignored going forward
- `.env.example` (template) can be safely committed
- You need to remove the env files from Git tracking with the commands above

---

**IMPORTANT:** After cleanup, rotate any credentials that were exposed in those files!
