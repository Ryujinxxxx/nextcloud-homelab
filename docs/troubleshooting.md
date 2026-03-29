# Troubleshooting Guide

## Issue: Git push failed
Solution:
- Ensure remote is configured
- Use Personal Access Token instead of password

## Issue: Permission denied (Nextcloud)
Solution:
- Check ownership:
  sudo chown -R www-data:www-data /mnt/nextcloud-data

## Issue: Docker not running
Solution:
- Restart Docker:
  sudo systemctl restart docker

## Issue: Cannot access Nextcloud
Solution:
- Check container status:
  docker ps
- Verify port 8080 is open

## Issue: Data not persisting
Solution:
- Verify volume mapping:
  /mnt/nextcloud-data:/var/www/html/data

## Issue: WSL storage confusion
Solution:
- Avoid using `/mnt/c/...` for production
- Use Linux-native paths or Raspberry Pi
