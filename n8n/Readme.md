# n8n Docker Setup

## Overview
This directory contains the Docker Compose configuration for running n8n workflow automation platform in a containerized environment.

## Prerequisites
- Docker installed and running
- Docker Compose installed

## Installation and Setup Guide

### Step 1: Navigate to the n8n Directory
```bash
cd /path/to/my_docker_container/n8n
```

### Step 2: Create Data Directory (if not exists)
```bash
mkdir -p ./n8n_data
```

### Step 3: Set Correct Permissions
```bash
# Set ownership for n8n data directory
sudo chown -R 1000:1000 ./n8n_data
```

### Step 4: Start n8n Service
```bash
# Start n8n in detached mode
docker-compose up -d
```

### Step 5: Verify Service is Running
```bash
# Check if n8n container is running
docker-compose ps
```
You should see the `n8n` container with status "Up".

### Step 6: Access n8n UI
- **Host**: localhost
- **Port**: 5678
- **URL**: http://localhost:5678
- **First-time Setup**: Create your admin account on first access

### Step 7: Create Your First Workflow
1. Click "Add workflow" in the n8n UI
2. Add nodes by clicking the "+" button
3. Configure each node's parameters
4. Connect nodes by dragging from one to another
5. Test your workflow using the "Test Workflow" button
6. Save and activate your workflow

### Step 8: Configure Webhooks (Optional)
If using webhooks, update the `WEBHOOK_URL` in `docker-compose.yaml`:
```yaml
- WEBHOOK_URL=https://your-domain.com/
```

## Project Structure
```
n8n/
├── n8n_data/       # Persistent data (workflows, credentials, settings)
│   └── config      # n8n configuration file
└── docker-compose.yaml
```

## Common Commands
```bash
# View logs
docker-compose logs -f n8n

# Stop service
docker-compose down

# Restart service
docker-compose restart

# Update to latest version
docker-compose pull
docker-compose up -d

# Check running containers
docker ps
```

## Configuration
Key environment variables in `docker-compose.yaml`:
- **Timezone**: Asia/Bangkok
- **Host**: localhost
- **Port**: 5678
- **Protocol**: http
- **Webhook URL**: http://localhost:5678/
- **User**: 1000:1000 (prevents permission issues)

## Backup Your Data
```bash
# Create backup of n8n data
tar -czf n8n_backup_$(date +%Y%m%d).tar.gz ./n8n_data/

# Restore from backup
tar -xzf n8n_backup_YYYYMMDD.tar.gz
```

## Troubleshooting

### Permission Denied Errors
```bash
sudo chown -R 1000:1000 ./n8n_data
```

### Container Won't Start
```bash
# Check logs
docker-compose logs n8n

# Remove container and restart
docker-compose down
docker-compose up -d
```

## Documentation
- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community](https://community.n8n.io/)
- [Docker Compose Reference](https://docs.docker.com/compose/compose-file/)