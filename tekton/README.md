# Tekton Pipelines for Spring Boot Hello World

This directory contains Tekton pipeline definitions for building, testing, and deploying the Spring Boot Hello World application.

## Pipeline Overview

### 1. Full Pipeline (`pipeline.yaml`)
A comprehensive pipeline that includes:
- Git repository cloning
- Maven build and testing
- Security scanning with Trivy
- Docker image building with Kaniko
- Image pushing to GitHub Container Registry
- Kubernetes deployment
- Integration testing

### 2. Simple Pipeline (`simple-pipeline.yaml`)
A simplified pipeline for basic CI/CD:
- Git repository cloning
- Maven build and testing
- Docker image building
- Basic application testing

## Prerequisites

1. **Tekton Installation**: Ensure Tekton is installed in your Kubernetes cluster
2. **Required Tasks**: Install the following Tekton tasks:
   - `git-clone`
   - `maven`
   - `kaniko`
   - `kubectl-apply`
   - `curl`

## Installation

### Install Required Tasks

```bash
# Install git-clone task
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/git-clone/0.9/git-clone.yaml

# Install maven task
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/maven/0.2/maven.yaml

# Install kaniko task
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/kaniko/0.6/kaniko.yaml

# Install kubectl-apply task
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/kubectl-apply/0.2/kubectl-apply.yaml

# Install curl task
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/curl/0.2/curl.yaml
```

### Create Namespace and Resources

```bash
# Create namespace
kubectl apply -f k8s/namespace.yaml

# Create GitHub Container Registry secret (if needed)
kubectl create secret docker-registry ghcr-secret \
  --docker-server=ghcr.io \
  --docker-username=YOUR_GITHUB_USERNAME \
  --docker-password=YOUR_GITHUB_TOKEN \
  --namespace=spring-boot-hello-world
```

## Usage

### Run the Simple Pipeline

```bash
# Apply the pipeline
kubectl apply -f tekton/simple-pipeline.yaml

# Run the pipeline
kubectl apply -f tekton/simple-pipeline-run.yaml
```

### Run the Full Pipeline

```bash
# Apply the pipeline
kubectl apply -f tekton/pipeline.yaml

# Run the pipeline
kubectl apply -f tekton/pipeline-run.yaml
```

## Monitoring

### Check Pipeline Status

```bash
# List pipeline runs
kubectl get pipelineruns

# Get detailed status
kubectl describe pipelinerun <pipeline-run-name>

# View logs
kubectl logs -f pipelinerun/<pipeline-run-name>
```

### Check Task Status

```bash
# List task runs
kubectl get taskruns

# Get task run details
kubectl describe taskrun <task-run-name>
```

## Pipeline Stages

### Simple Pipeline Stages:
1. **fetch-repository**: Clone the Git repository
2. **maven-build**: Build and test with Maven
3. **build-image**: Create Docker image with Kaniko
4. **test-application**: Test the application endpoints

### Full Pipeline Stages:
1. **fetch-repository**: Clone the Git repository
2. **maven-build**: Build and test with Maven
3. **security-scan**: Run Trivy security scan
4. **build-image**: Create Docker image
5. **push-image**: Push to GitHub Container Registry
6. **deploy-to-k8s**: Deploy to Kubernetes
7. **integration-tests**: Run integration tests

## Configuration

### Environment Variables

The pipelines use the following environment variables:
- `GITHUB_TOKEN`: GitHub personal access token for registry access
- `GITHUB_USERNAME`: GitHub username for registry access

### Customization

You can customize the pipelines by modifying:
- **Git repository URL**: Change `git-url` parameter
- **Docker image name**: Modify `image-name` parameter
- **Maven goals**: Adjust the `GOALS` parameter in maven-build task
- **Kubernetes namespace**: Update namespace references

## Troubleshooting

### Common Issues

1. **Task Not Found**: Ensure all required tasks are installed
2. **Permission Denied**: Check service account permissions
3. **Image Push Failed**: Verify registry credentials
4. **Build Timeout**: Increase timeout values for large builds

### Debug Commands

```bash
# Check Tekton installation
kubectl get pods -n tekton-pipelines

# Verify tasks are available
kubectl get tasks

# Check pipeline status
kubectl get pipelineruns -o wide

# View detailed logs
kubectl logs -f deployment/tekton-pipelines-controller -n tekton-pipelines
```

## Integration with Backstage

The Tekton pipelines integrate with Backstage through:
- Pipeline status monitoring
- Build artifact tracking
- Deployment status updates
- Integration with GitHub Actions workflows

## Security Considerations

- Use non-root containers
- Implement proper RBAC
- Secure registry credentials
- Enable security scanning
- Use read-only file systems where possible