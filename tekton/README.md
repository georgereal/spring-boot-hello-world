# Tekton Pipeline for Spring Boot Hello World

This directory contains Tekton pipeline configurations for building and testing the Spring Boot Hello World application.

## Pipeline Overview

### spring-boot-build-test-pipeline
A simplified pipeline that builds and tests the Spring Boot application without Docker build/push steps.

**Tasks:**
1. **fetch-repository**: Clones the GitHub repository
2. **maven-build**: Builds the Spring Boot application using Maven
3. **test-application**: Tests the application endpoints (currently disabled due to localhost access)

## Files

- `pipeline.yaml` - Comprehensive pipeline with Docker build/push
- `simple-pipeline.yaml` - Simplified pipeline with Docker build
- `build-test-pipeline.yaml` - Basic build and test pipeline (recommended)
- `pipeline-run.yaml` - Pipeline run for the comprehensive pipeline
- `simple-pipeline-run.yaml` - Pipeline run for the simple pipeline
- `build-test-pipeline-run.yaml` - Pipeline run for the build-test pipeline
- `custom-maven-task.yaml` - Custom Maven task for Java 11 compatibility

## Backstage Integration

The pipeline is integrated with Backstage through the following catalog entities:

### Main Component (catalog-info.yaml)
- Updated with Tekton pipeline annotations
- Includes links to Tekton Dashboard
- Shows pipeline status and information

### Tekton Component (tekton-catalog-info.yaml)
- Dedicated Tekton pipeline entity
- Provides detailed pipeline information
- Links to pipeline runs and dashboard

## Usage

### Running the Pipeline

```bash
# Apply the custom Maven task
kubectl apply -f tekton/custom-maven-task.yaml

# Apply the pipeline
kubectl apply -f tekton/build-test-pipeline.yaml

# Run the pipeline
kubectl apply -f tekton/build-test-pipeline-run.yaml
```

### Monitoring

```bash
# Check pipeline run status
kubectl get pipelineruns

# Check task run status
kubectl get taskruns

# View pipeline logs
kubectl logs <pipeline-run-pod-name>
```

### Backstage UI

1. Navigate to the Spring Boot Hello World component in Backstage
2. View the Tekton tab to see pipeline information
3. Access pipeline runs and logs
4. Use the provided links to access Tekton Dashboard

## Configuration

### Pipeline Parameters
- `git-url`: GitHub repository URL (default: https://github.com/georgereal/spring-boot-hello-world.git)

### Workspaces
- `shared-workspace`: Persistent volume claim for sharing data between tasks

### Maven Configuration
- Java version: 11
- Spring Boot version: 2.7.18
- Maven goals: clean, package

## Troubleshooting

### Common Issues

1. **Maven Build Fails**: Ensure the custom Maven task is applied
2. **Image Pull Errors**: Check if the Maven image exists locally
3. **Pipeline Validation**: Verify all required tasks are available in the cluster

### Logs

```bash
# Get pipeline run logs
kubectl logs <pipeline-run-name>-<task-name>-pod

# Describe pipeline run for more details
kubectl describe pipelinerun <pipeline-run-name>
```

## Next Steps

1. Configure Docker registry credentials for image building
2. Add more comprehensive testing tasks
3. Implement deployment tasks for Kubernetes
4. Set up webhook triggers for automatic pipeline execution