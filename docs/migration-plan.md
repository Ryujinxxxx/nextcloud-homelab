# Migration Plan

## Objective

Migrate Nextcloud deployment from WSL prototype to Raspberry Pi production environment using external HDD.

## Current State
- WSL Ubuntu
- Docker-based testing
- No persistent production storage

## Target State
- Raspberry Pi host
- External HDD mounted at `/mnt/nextcloud-data`
- Docker-based Nextcloud deployment
- Cloudflare Tunnel for secure access

## Steps

1. Prepare Raspberry Pi OS / Ubuntu Server
2. Connect external HDD
3. Format HDD to ext4
4. Mount HDD to `/mnt/nextcloud-data`
5. Configure auto-mount using `/etc/fstab`
6. Install Docker and Docker Compose
7. Deploy Nextcloud stack
8. Configure Cloudflare Tunnel
9. Validate file upload/download
10. Implement backup strategy

## Risks
- Incorrect mount configuration
- Permission issues
- Data loss if HDD not handled properly

## Mitigation
- Use UUID for mount
- Test read/write before deployment
- Backup initial data
