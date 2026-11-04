# Full-Stack Chat Application – DevOps Implementation on GKE

A real-time chat application containerized with Docker and deployed on **Google Kubernetes Engine (GKE)** using Kubernetes manifests and a GitHub Actions CI/CD pipeline.

This project focuses on DevOps implementation, including containerization, Kubernetes orchestration, automated CI/CD, code quality analysis, image vulnerability scanning, and deployment to Google Cloud Platform.

> **Contribution Note:** The original application code was developed separately. My contribution focuses on Docker containerization, Kubernetes deployment, GCP infrastructure integration, and CI/CD automation.

## Architecture

```text
              Developer
                  |
                  v
             GitHub Push
                  |
                  v
          GitHub Actions Runner
                  |
          +-------+--------+
          |                |
          v                v
      SonarQube          Docker Build
     Code Analysis      Frontend/Backend
                           |
                           v
                      Trivy Scan
                           |
                           v
                  Google Artifact Registry
                           |
                           v
                    GKE Deployment
                           |
                 +---------+---------+
                 |                   |
                 v                   v
             Frontend             Backend
             (Nginx)           (Node.js/Express)
                                     |
                                     v
                                  MongoDB
```

## Technology Stack

| Category | Technologies |
|---|---|
| Cloud Platform | Google Cloud Platform |
| CI/CD | GitHub Actions |
| Authentication | Workload Identity Federation (WIF) |
| Containerization | Docker |
| Container Registry | Google Artifact Registry |
| Orchestration | Kubernetes, GKE |
| Web Server | Nginx |
| Code Quality | SonarQube |
| Image Security | Trivy |
| Application | React, Node.js, Express |
| Database | MongoDB |
| Real-time Communication | Socket.IO |

## Application Features

- Real-time messaging using Socket.IO
- JWT-based authentication
- User profile management
- Online/offline user status
- React and Tailwind CSS frontend
- Node.js and Express backend
- MongoDB database

## DevOps Implementation

### 1. Docker Containerization

- Created separate Docker images for frontend and backend.
- Containerized the application components.
- Used Docker to build and run application containers.
- Prepared images for deployment to Kubernetes.

### 2. Google Artifact Registry

- Created an Artifact Registry repository in GCP.
- Configured Docker authentication with Google Cloud CLI.
- Pushed frontend and backend images to Artifact Registry.
- Used Git commit SHA tags for version-specific images.

### 3. Kubernetes Deployment on GKE

- Deployed the application on Google Kubernetes Engine.
- Created Kubernetes Deployments and Services.
- Configured MongoDB using StatefulSet and persistent storage.
- Used ConfigMaps and Secrets for application configuration.
- Configured Ingress for external application access.

### 4. GitHub Actions CI/CD Pipeline

Automated the application build and deployment process using GitHub Actions.

Pipeline stages:

1. Checkout source code.
2. Run SonarQube code analysis for frontend and backend.
3. Build frontend and backend Docker images.
4. Scan container images using Trivy.
5. Authenticate to GCP using Workload Identity Federation.
6. Push images to Google Artifact Registry.
7. Connect to the GKE cluster.
8. Update Kubernetes Deployments with the new image tags.
9. Verify deployment using Kubernetes rollout status.

### 5. Security Implementation

- Used Workload Identity Federation instead of storing GCP service account keys in GitHub.
- Used GitHub Secrets for sensitive configuration such as SonarQube credentials.
- Integrated SonarQube for static code analysis.
- Integrated Trivy for container image vulnerability scanning.
- Used Kubernetes Secrets for sensitive application configuration.

## GCP Configuration

| Resource | Configuration |
|---|---|
| Project ID | `double-backup-509612-i1` |
| Artifact Registry Region | `asia-south1` |
| Artifact Registry Repository | `image-hub` |
| GKE Cluster | `cluster-1` |
| Cluster Location | `asia-south1-a` |
| Kubernetes Namespace | `app` |

## Repository Structure

```text
full-stack_chatApp/
│
├── .github/
│   └── workflows/
│       └── CI/CD workflow
│
├── backend/
│   └── Backend application and Dockerfile
│
├── frontend/
│   └── Frontend application and Dockerfile
│
├── k8s/
│   └── Kubernetes manifests
│
├── docker-compose.yml
├── package.json
└── README.md
```

## Useful Kubernetes Commands

Check application Pods:

```bash
kubectl get pods -n app
```

Check Services:

```bash
kubectl get svc -n app
```

Check Deployments:

```bash
kubectl get deployments -n app
```

Check Ingress:

```bash
kubectl get ingress -n app
```

Check deployment rollout:

```bash
kubectl rollout status deployment/frontend -n app
kubectl rollout status deployment/backend -n app
```

## CI/CD Deployment Strategy

The pipeline uses Git commit SHA as the Docker image tag.

Example:

```text
frontend:<github-commit-sha>
backend:<github-commit-sha>
```

This helps identify which application version is deployed and makes rollbacks easier.

## Learning Outcomes

Through this project, I gained practical experience with:

- Docker image creation and containerization.
- Kubernetes Deployments, Services, StatefulSets and Ingress.
- GKE cluster deployment and management.
- Google Artifact Registry.
- GitHub Actions CI/CD automation.
- GCP authentication using Workload Identity Federation.
- SonarQube code quality analysis.
- Trivy container vulnerability scanning.
- Automated Kubernetes application deployments.

## License

The application repository includes an MIT License. Refer to the [LICENSE](LICENSE) file for details.

## Repository

[GitHub – Full-Stack Chat Application](https://github.com/sandesh-kumar00/full-stack_chatApp.git)
