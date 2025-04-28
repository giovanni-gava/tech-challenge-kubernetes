# DevOps Kubernetes Task

## Application Details

Our great log application can't persistently store data in Postgres. Please fix it. 🙏😺

The application is a python job hosted on Kubernetes. You need to set up the Kubernetes "cluster" using k3s and Docker Compose.

## How to Run

1. **Start the K3S containers:**

   ```bash
   docker compose up -d
   ```

2. **Access the running container:**

   ```bash
   docker compose exec k3s-server sh
   ```

3. **Apply the Kubernetes manifests using Kustomize inside the container:**

   ```bash
   kubectl apply -k ./manifests/
   ```

   You can modify files in the `manifests` directory and reapply them using the command above.

## How to Test

To verify that the task is finished correctly, you need to be sure that the python job is writing logs to the Postgres database
and this information is still available after Postgres pod restart.
You can execute into PG pod and check the logs table in testdb database.

### Tips

How to restart python job quicly
```bash
./manifests/restart_job.sh
```
