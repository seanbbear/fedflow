# Deploy to GitHub Pages

## 1) Initialize git (one time)

```bash
cd /Users/sean.peng/Desktop/fedflow
git init -b main
git add .
git commit -m "init: fedflow prototype"
```

## 2) Create GitHub repo and push

Replace `<YOUR_GITHUB_REPO_URL>` with your repository URL.

```bash
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

## 3) Enable GitHub Pages (Actions)

In GitHub repo:
1. `Settings` -> `Pages`
2. `Build and deployment` -> `Source`: choose `GitHub Actions`

After push, workflow `Deploy static site to GitHub Pages` runs automatically.

## 4) Open your site

URL format:

```text
https://<your-username>.github.io/<repo-name>/
```

## Notes

- This project currently uses `localStorage`, so saved flows are browser/device specific.
- Public multi-user shared data requires a backend/database.
