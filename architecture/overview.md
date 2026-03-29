# Architecture Overview

## System Design

This project follows a hybrid homelab architecture where the development environment is built in WSL and the production environment is designed for Raspberry Pi with external HDD.

## High-Level Architecture

User → Cloudflare Tunnel → Raspberry Pi → Docker → Nextcloud + MariaDB → External HDD

## Components

### 1. Compute Layer
- Raspberry Pi (planned production host)
- WSL Ubuntu (development environment)

### 2. Application Layer
- Nextcloud (file storage and collaboration)
- MariaDB (database backend)

### 3. Storage Layer
- External HDD mounted at `/mnt/nextcloud-data`
- Ensures data persistence independent from OS

### 4. Network Layer
- Cloudflare Tunnel for secure remote access
- No direct port exposure

## Design Decisions

### Why not WSL for production?
- Virtualized storage
- Unstable for persistent workloads
- Performance and permission issues

### Why Docker?
- Portable deployment
- Easy environment replication
- Clean separation of services

### Why External HDD?
- Avoid SSD wear
- Better scalability for storage
- Production-like storage separation

## Future Enhancements
- S3 backup integration
- Monitoring (Prometheus + Grafana)
- Kubernetes deployment (EKS / K3s)
