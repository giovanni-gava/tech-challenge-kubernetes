# Tech Challenge: Kubernetes Log Application

## Overview

This project runs a Python job in Kubernetes that inserts data into a PostgreSQL database.  
It simulates the behavior of log persistence across pod restarts.

## Architecture

- Kubernetes cluster via k3s (Docker Compose)
- Python job container (psycopg2)
- PostgreSQL database (StatefulSet)

## How to Run

1. Start the cluster:

    ```bash
    docker compose up -d
    ```

2. Enter the server container:

    ```bash
    docker compose exec k3s-server sh
    ```

3. Deploy resources:

    ```bash
    kubectl apply -k ./manifests/
    ```

## How to Test

1. Check Python job logs.
2. Restart PostgreSQL pod:

    ```bash
    kubectl delete pod <postgresql-pod-name>
    ```

3. Verify logs persist:

    ```bash
    kubectl exec -it <postgresql-pod-name> -- psql -U postgres -d testdb
    SELECT * FROM logs;
    ```

## Quick Job Restart

```bash
./manifests/restart_job.sh
