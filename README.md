# TAK Server Sample Applications

This repository contains sample applications and deployment configurations for TAK (Tactical Assault Kit) Server, a situational awareness and communication platform.

## Overview

TAK Server is an open-source platform for real-time situational awareness and communication. This repository provides:

- Docker container configurations for TAK Server and its PostgreSQL database
- Kubernetes manifests for deploying to a K8s cluster
- Helm chart for easy deployment and management
- Sample configurations and scripts

## Directory Structure

```
apg-sample-apps/
├── docker/                 # Dockerfiles for building TAK Server images
├── helm/                   # Helm chart for Kubernetes deployment
├── k8s/                    # Raw Kubernetes manifests
├── src/                    # TAK Server source code and configurations
├── .gitignore             # Git ignore rules
└── README.md              # This file
```

## Prerequisites

- Docker and Docker Compose
- Kubernetes cluster (for K8s deployment)
- Helm 3 (for Helm deployment)
- Java 17+ (for local development)

## Building the Docker Images

From the repository root:

```bash
# Build TAK Server image
docker build -f Dockerfile.takserver -t takserver:latest .

# Build TAK Server DB image
docker build -f Dockerfile.takserver-db -t takserver-db:latest .
```

## Running Locally with Docker

1. Build the images as above
2. Run the containers:

```bash
docker run -d --name tak-db takserver-db:latest
docker run -d --name tak-server -p 8443:8443 --link tak-db takserver:latest
```

## Kubernetes Deployment

### Using Raw Manifests

```bash
cd k8s
kubectl apply -f namespace.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f pvc.yaml
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml
kubectl apply -f takserver-deployment.yaml
kubectl apply -f takserver-service.yaml
kubectl apply -f httproute.yaml
```

### Using Helm Chart

```bash
cd helm/tak-server
helm install tak-server .
```

## Configuration

- Edit `src/CoreConfig.xml` for TAK Server configuration
- Update secrets in `k8s/secret.yaml` or `helm/tak-server/values.yaml`
- Modify environment variables in the deployment manifests

## Ports

- 8089: TLS input
- 8443: HTTPS web interface
- 8444: Federation HTTPS
- 8446: Certificate HTTPS

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is licensed under the terms specified in the TAK Server license.

## Support

For support and documentation, refer to the official TAK Server documentation or community forums.