Here is a **proper technical note/document** 👇

---

# 📘 GitHub → GitLab Auto Sync (Force Mirror) Documentation

## 🎯 Objective

Automatically sync code from **GitHub main branch** to **GitLab repository**.
Whenever code is pushed to GitHub, it will **fully replace** GitLab code (force mirror).

No merge required. GitHub is **main source of truth**.

---

# 🏗 Architecture Flow

Developer Push → GitHub (main) → GitHub Action → Force Push → GitLab (main)

GitLab repo always mirrors GitHub.

---

# 🔐 Requirements

## 1️⃣ GitLab Personal Access Token

Create token from GitLab:

**GitLab → Profile → Access Tokens**

Enable permissions:

- ✅ write_repository
- ✅ read_repository

Copy token.

---

## 2️⃣ Add Token in GitHub Secrets

Go to GitHub repo:

Settings → Secrets & variables → Actions → New repository secret

```
Name: GITLAB_TOKEN
Value: <your_gitlab_token>
```

Save.

---

# 📂 GitHub Action Workflow File

Create file:

```
.github/workflows/github-to-gitlab.yml
```

Or your current path:

```
/home/uysys/Developement/UYSYS/smartflow-v2/github-to-gitlab.yml
```

---

# ⚙️ Final Working YAML

```yaml
name: Sync GitHub to GitLab

on:
  push:
    branches:
      - main

jobs:
  sync:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout GitHub repo
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Configure Git
        run: |
          git config user.name "github-actions"
          git config user.email "github-actions@github.com"

      - name: Force push to GitLab (Mirror)
        run: |
          git remote add gitlab https://oauth2:${{ secrets.GITLAB_TOKEN }}@gitlab.a2i.gov.bd/testproject/test.git
          git push gitlab main --force
```

---

# 🚀 How It Works

### Step 1

Developer pushes code to GitHub main branch.

### Step 2

GitHub Action triggers automatically.

### Step 3

Workflow:

- Checkout repo
- Add GitLab remote
- Force push to GitLab

### Step 4

GitLab repo fully replaced by GitHub code.

---

# 🛑 Important Notes

## 1. GitLab Branch Protection

If error:

```
You are not allowed to force push to protected branch
```

### Fix:

GitLab → Settings → Repository → Protected Branches
Remove protection OR allow force push.

---

## 2. Force Push Warning

This will:

- ❌ Delete GitLab old code
- ❌ Remove GitLab commits
- ✅ Fully replace with GitHub

GitHub becomes master source.

---

## 3. If First Push Fails

If error:

```
fetch first / rejected
```

Use force push (already added).

---

# 🧪 Testing Steps

1. Push any commit to GitHub main
2. Go to GitHub → Actions tab
3. Check workflow running
4. Open GitLab repo
5. Confirm updated code

---

# 🧰 Troubleshooting

## Error: repository not found

Check:

- GitLab repo URL
- Token permission
- Project access

## Error: protected branch

Disable protection or allow force push.

---

# 🏁 Final Result

✔ GitHub main → auto deploy to GitLab
✔ No manual push needed
✔ Fully mirrored
✔ CI/CD ready

---

# 📌 Suggested Use (For your company)

Good for:

- Government projects (a2i, mygov)
- Client mirror repo
- Backup repo
- Deployment repo

---

## Need advanced version?

Tell me I will give you:

- Auto deploy to server after GitLab
- Multi-branch sync
- GitHub → GitLab → Server pipeline
- CI/CD production setup (DevOps level)
