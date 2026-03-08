# TAK Server Kubernetes Deployment

This directory contains Kubernetes manifests to deploy TAK Server on a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster
- kubectl configured
- Docker images built and pushed to registry:
  - takserver:latest (build from docker/Dockerfile.takserver)
  - takserver-db:latest (build from docker/Dockerfile.takserver-db)

## Building Images

From the apg-sample-apps directory:

```bash
docker build -f docker/Dockerfile.takserver -t takserver:latest .
docker build -f docker/Dockerfile.takserver-db -t takserver-db:latest .
```

Push to your registry as needed.

## Deployment Steps

1. Update the ConfigMap with your actual CoreConfig.xml
2. Update the Secret with actual passwords and certificates
3. Build and push Docker images
4. Apply the manifests:

```bash
kubectl apply -f namespace.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f pvc.yaml
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml
kubectl apply -f takserver-deployment.yaml
kubectl apply -f takserver-service.yaml
kubectl apply -f ingress.yaml
```

5. Wait for pods to be ready
6. Access the application via the Ingress host

## Notes

- This is a basic setup. Adjust resources, replicas, etc., as needed.
- Persistence is set up for DB data.
- Multi-process app may need refinement for production.