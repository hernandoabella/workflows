🌿 Git Workflow
# 🌿 Git Workflow

A simple and scalable Git workflow for daily development, collaboration, and releases.

---

## 1️⃣ Main Branches

| Branch | Purpose |
|------|--------|
| `main` | Production-ready code |
| `develop` | Integration branch for features |
| `feature/*` | New features |
| `fix/*` | Bug fixes |
| `hotfix/*` | Urgent production fixes |
| `release/*` | Release preparation |

---

## 2️⃣ Branch Naming Convention

```txt
feature/login-form
feature/payment-integration
fix/navbar-overflow
hotfix/security-patch
release/v1.2.0

3️⃣ Start a New Feature
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name


Work normally and commit often:

git add .
git commit -m "feat: add login form"

4️⃣ Keep Branch Updated
git fetch origin
git rebase origin/develop


(Use merge instead of rebase if your team prefers.)

5️⃣ Open a Pull Request

Base branch: develop

Use clear PR titles

Describe what and why

Add screenshots if UI-related

Request at least one review

6️⃣ Merge Rules

✅ All checks must pass

✅ No direct commits to main

✅ Squash or rebase commits when merging

❌ No broken builds

7️⃣ Release Flow
git checkout develop
git checkout -b release/v1.2.0


Update version numbers

Update changelog

Final testing

Merge release into main:

git checkout main
git merge release/v1.2.0
git tag v1.2.0
git push origin main --tags


Then back into develop:

git checkout develop
git merge release/v1.2.0

8️⃣ Hotfix Flow
git checkout main
git checkout -b hotfix/critical-bug


Fix → commit → merge back:

git checkout main
git merge hotfix/critical-bug
git tag v1.2.1
git push origin main --tags


Also merge into develop:

git checkout develop
git merge hotfix/critical-bug

9️⃣ Commit Message Convention (Recommended)
feat: new feature
fix: bug fix
chore: tooling or config
docs: documentation
refactor: code refactor
test: tests


Example:

git commit -m "fix: prevent form submit duplication"

🔒 Best Practices

Pull before you push

Small, focused commits

Never commit secrets

Use .gitignore

Review before merging

🔁 Workflow Variations

This workflow can be adapted for:

Solo projects (skip develop)

Small teams

Large teams with CI/CD

Open-source projects

✅ Works With

GitHub Flow

GitLab Flow

Bitbucket

CI/CD pipelines
