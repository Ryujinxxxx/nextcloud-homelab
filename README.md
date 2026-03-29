# Nextcloud Homelab Journey: WSL Prototype to Raspberry Pi + External HDD

## 📊 Architecture

This project includes two architecture views:

- [Interactive HTML Diagram](./architecture/interactive-diagram.html)
- [GitHub Mermaid Diagram](./architecture/diagram.md)

<img width="795" height="587" alt="image" src="https://github.com/user-attachments/assets/5ac4b61c-78a5-47f8-9277-41c18d7cd9c3" />


The HTML version is more polished and clickable. The Mermaid version renders directly in GitHub.

## Project Overview

This project documents my self-hosted cloud storage journey using Ubuntu on WSL, Docker, Cloudflare Tunnel, and a planned migration to Raspberry Pi with external HDD for a cleaner production-style setup.

The goal is not just to make Nextcloud run, but to build a real homelab / cloud engineering project that demonstrates:

- Linux administration
- Docker-based deployment
- Storage architecture planning
- Secure remote access using Cloudflare Tunnel
- Migration design from development environment to production hardware
- Documentation and troubleshooting mindset

---

## Current Status

### Phase 1 — WSL Prototype
I used Ubuntu on WSL to begin testing and learning the deployment flow.

What I have done so far:

- Set up Ubuntu in WSL on my local Windows machine
- Worked from the WSL environment under the host machine `Ryujin`
- Installed and used Docker
- Confirmed Docker storage is active in WSL
- Explored using a local Windows drive path for storage
- Investigated where Nextcloud files and data should live
- Evaluated the limitations of WSL for production storage use
- Planned secure exposure of services using Cloudflare Tunnel
- Decided not to use the internal SSD as the long-term data location
- Decided to migrate the project to Raspberry Pi + external HDD

### Phase 2 — Production Direction
The final target architecture is:

- Raspberry Pi as the host
- External HDD as the primary data storage
- Nextcloud in Docker
- Cloudflare Tunnel for secure external access
- Optional future improvements such as monitoring, backups, and hybrid cloud sync

---

## Why I Am Moving Away from WSL

WSL was useful for learning and testing, but it is not the best long-term host for this project.

Main reasons:
- WSL storage devices are virtualized
- It is difficult to guarantee real HDD-only storage usage
- Windows-mounted paths such as `/mnt/d/...` can introduce permission issues, slower I/O, and file locking inconsistencies
- It is not ideal for a stable, always-on self-hosted service

Because of this, I decided to use WSL as a prototype and learning environment, then migrate to Raspberry Pi + external HDD for the actual deployment.

---

## Architecture Summary

### Current Prototype Architecture (WSL)

- Windows PC
- WSL Ubuntu
- Docker Engine
- Nextcloud container planned/tested
- Cloudflare Tunnel planned
- Windows-mounted storage only for testing

### Target Production Architecture (Raspberry Pi)

- Internet user
- Cloudflare Tunnel
- Raspberry Pi
- Docker Engine
- Nextcloud container
- MariaDB container
- External HDD mounted at `/mnt/nextcloud-data`

---

## Proposed Production Architecture Details

### Compute Layer
- Host: Raspberry Pi
- Operating System: Raspberry Pi OS or Ubuntu Server
- Container Runtime: Docker + Docker Compose

### Application Layer
- Nextcloud container for file access, sync, sharing, and web UI
- MariaDB container for database

### Storage Layer
- External HDD mounted to Linux, for example:
  - `/mnt/nextcloud-data`

This ensures user files are stored on the HDD, not the SSD or SD card.

### Secure Access Layer
- Cloudflare Tunnel
- Domain-based secure access without direct port exposure

### Future Enhancements
- Automatic backup to another disk or cloud object storage
- Monitoring using Netdata, Prometheus, or Grafana
- Scheduled backup and recovery testing
- Optional hybrid sync to AWS S3

---

## Important Technical Findings

### 1. WSL is good for testing, not ideal for production storage
During testing, I confirmed that WSL does not behave like a normal physical Linux server when it comes to storage devices. The disk view is virtualized, which makes it unsuitable for enforcing a true HDD-only architecture.

### 2. Storage location matters
A self-hosted storage platform must clearly separate:
- application code
- container runtime
- persistent user data

That is why the final design uses:
- Raspberry Pi for compute
- external HDD for persistent data

### 3. Architecture decisions are as important as installation
This project became more than just installing Nextcloud. It required evaluating filesystem placement, long-term maintainability, data safety, production suitability, and access security.

---

## Recommended Folder Layout for Production

```bash
/opt/nextcloud
/mnt/nextcloud-data
/mnt/nextcloud-db

