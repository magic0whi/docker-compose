# Homelab / Self-Hosted Docker Services

This repository contains a collection of Docker Compose configurations and setup scripts for various self-hosted services.

## Overview of Services

This repository provides containerized deployments for the following applications:

- **[Aria2 Pro](aria2-pro-docker-p3terx/)**: A powerful aria2 Docker image by P3TERX for downloading files.
- **[DDClient](ddclient-linuxserver/)**: A Perl client used to update dynamic DNS entries for accounts on Dynamic DNS Network Service Providers (configured for Cloudflare).
- **[Hentai@Home](hah/)**: A Java-based peer-to-peer gallery distribution client.
- **[Mailserver](mailserver/)**: A full-featured mail server deployment using docker-mailserver.
- **[Minecraft](minecraft-itzg/)**: A Minecraft server running via the popular itzg Docker image.
- **[Papra](papra/)**: Papra docker compose deployment.
- **[Plane](plane/)**: An open-source project management tool.
- **[Qinglong](qinglong/)**: A cron task management platform supporting Python3, JavaScript, Shell, and Typescript.
- **[Samba DC](samba-dc/)**: Active Directory Domain Controller based on Samba.

## Repository Structure

Each service has its own dedicated directory containing the necessary `docker-compose.yml`, `.env` templates, configuration files, and utility scripts.

```plaintext
.
├── all-down.sh                 # Script to quickly spin down all services
├── aria2-pro-docker-p3terx/    # Aria2 Pro download manager configuration
├── ddclient-linuxserver/       # Dynamic DNS updater configuration
├── hah/                        # Hentai@Home client configuration
├── mailserver/                 # Full mail server stack and scripts
├── minecraft-itzg/             # Minecraft server deployment
├── papra/                      # Papra service
├── plane/                      # Plane project management setup
├── qinglong/                   # Qinglong task manager
└── samba-dc/                   # Samba Domain Controller config zones
```

## Quick Start

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed.
- [Docker Compose](https://docs.docker.com/compose/install/) (v2 recommended).
- Proper file permissions and external storage mounted if necessary (e.g., `/mnt/storage2/`, `/mnt/storage3/`).

### Standard Deployment

1. Navigate to the desired service's directory:
   ```bash
   cd <service_directory>
   ```
2. Copy the sample environment/configuration files and populate them with your secrets:
   - Example: Copy `secret.env.sample` to `secret.env` (if applicable) and fill in your details.
3. Start the service in detached mode:
   ```bash
   docker compose up -d
   ```

### Service-Specific Commands & Tips

#### Papra

To rebuild and start the Papra service using its specific environment file from the root directory, run:
```bash
docker compose -f papra/docker-compose.yml --env-file papra/secrets.env up -d --build
```

#### Plane (Makeplane)

To launch the orchestra for Plane with the required environment files from the root directory, run:
```bash
docker compose -f plane/docker-compose.yml --env-file plane/variables.env --env-file plane/secrets.env up -d
```

### Stopping All Services

You can use the provided `all-down.sh` script in the root directory to stop all running containers defined in this repository:

```bash
./all-down.sh
```

## Note on Storage Volumes

Many of these services are configured to mount specific host paths (e.g., `/mnt/storage3/aria2/downloads`, `/mnt/storage2/hath/data`). Make sure these directories exist on your host system and have the appropriate read/write permissions for the Docker user mapping, or modify the `docker-compose.yml` volumes to match your environment.
