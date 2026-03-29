# GitHub Update Guide

## 1. Check your files
Run:

ls

You should see:
- README.md
- GITHUB_UPDATE_GUIDE.md

## 2. Initialize git if needed

git init

## 3. Add the files

git add .

## 4. Commit

git commit -m "docs: add Nextcloud architecture and Raspberry Pi migration plan"

## 5. Connect to GitHub
If your repo is new:

git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/nextcloud-homelab.git
git push -u origin main

## 6. If remote already exists

git remote -v
git push origin main

## 7. If push is rejected

git pull origin main --rebase
git push origin main
