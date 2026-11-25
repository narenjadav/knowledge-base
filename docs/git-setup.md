# Git Setup and Everyday Commands

## 1. Configure Git (one-time setup)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

## 2. Sign in to GitHub

GitHub no longer accepts account passwords for Git over HTTPS. Use one of these instead:

**Option A: GitHub CLI (easiest)**

```bash
gh auth login        # follow the prompts, choose HTTPS
gh auth setup-git    # lets git use the same login
```

**Option B: SSH key**

```bash
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub   # add this key at GitHub → Settings → SSH and GPG keys
```

Then clone with the SSH URL (`git@github.com:<username>/<repo_name>.git`).

> Don't put a personal access token inside the clone URL (`https://<token>@github.com/...`). It gets saved in plain text in `.git/config` and your shell history.

## 3. Clone a repository

```bash
git clone <repository_url>
```

## 4. Stage files

```bash
git add <file1> <file2>   # specific files
git add .                 # everything in the current folder
```

## 5. Commit changes

```bash
git commit -m "Short description of the change"
```

## 6. Push changes

```bash
git push -u origin main   # first push sets the upstream
git push                  # after that
```

## 7. Add a remote (if the repo has none)

```bash
git remote add origin <repository_url>
git remote -v             # check it
```
