# Airflow Docker Setup

## Overview
This directory contains the Docker Compose configuration for running Apache Airflow in a containerized environment.

## Prerequisites
- Docker installed and running
- Docker Compose installed

## Installation and Setup Guide

### Step 1: Navigate to the Airflow Directory
```bash
cd /path/to/my_docker_container/airflow
```

### Step 2: Create Required Directories (if not exists)
```bash
mkdir -p ./dags ./logs ./plugins ./config
```

### Step 3: Set Environment Variables (Optional)
```bash
# Set Airflow UID (default: 50000)
export AIRFLOW_UID=50000
```

### Step 4: Initialize Airflow Database
```bash
# First time setup - initialize the database and create admin user
docker-compose up airflow-init
```
Wait for the initialization to complete. You should see "airflow-init exited with code 0".

### Step 5: Start All Services
```bash
# Start all Airflow services in detached mode
docker-compose up -d
```

### Step 6: Verify Services are Running
```bash
# Check if all containers are healthy
docker-compose ps
```
You should see `airflow-webserver`, `airflow-scheduler`, and `postgres` running.

### Step 7: Access Airflow UI
- **Host**: localhost
- **Port**: 8080
- **URL**: http://localhost:8080
- **Default Username**: airflow
- **Default Password**: airflow

### Step 8: Create Your First DAG
1. Place your DAG Python files in the `./dags/` directory
2. Example: `./dags/hello_world.py`
3. Airflow will automatically detect new DAGs (may take a few seconds)
4. Refresh the Airflow UI to see your DAG

### Step 9: Enable and Trigger a DAG
1. In the Airflow UI, find your DAG
2. Toggle the switch to enable it
3. Click the play button to trigger a manual run
4. Monitor execution in the UI

## Project Structure
```
airflow/
├── dags/           # DAG definitions
├── logs/           # Airflow logs
├── plugins/        # Custom plugins
├── config/         # Configuration files
└── docker-compose.yaml
```

## Common Commands
```bash
# View webserver logs
docker-compose logs -f airflow-webserver

# View scheduler logs
docker-compose logs -f airflow-scheduler

# Stop services
docker-compose down

# Reset database (removes all volumes)
docker-compose down -v

# Check running services and their ports
docker-compose ps
```

## Configuration
Modify environment variables in `docker-compose.yaml` to customize Airflow settings:
- **Database**: PostgreSQL (default user: jeerasak)
- **Executor**: LocalExecutor
- **Database Connection**: `postgresql+psycopg2://jeerasak:ghost2020@postgres/airflow`

## Documentation
- [Apache Airflow Docs](https://airflow.apache.org/docs/)
- [Docker Compose Reference](https://docs.docker.com/compose/compose-file/)