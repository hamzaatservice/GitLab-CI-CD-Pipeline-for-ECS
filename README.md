# GitLab CI/CD Pipeline for Oversee API (Staging Environment)

This repository contains the CI/CD pipeline configuration for the **Oversee API** staging environment. The pipeline automates building, pushing, and deploying the Docker container to AWS ECS using Amazon ECR.

## Workflow Overview

The CI/CD pipeline follows these steps:

1. **Build the Docker image** for the  API.
2. **Push the image** to the Amazon Elastic Container Registry (ECR).
3. **Deploy the image** to AWS ECS by updating the task definition and service.

## Prerequisites

Before running the pipeline, ensure the following:

1. **GitLab Runner** with Docker-in-Docker (DinD) support is available.
2. AWS CLI is installed and properly configured in the runner.
3. The necessary **IAM permissions** are assigned to the AWS credentials for:
   - Pushing Docker images to Amazon ECR.
   - Registering ECS task definitions.
   - Updating ECS services.

## Environment Variables

The following environment variables are required to run the pipeline. These should be configured as GitLab CI/CD variables:

| Variable                     | Description                                      |
|------------------------------|--------------------------------------------------|
| `AWS_REGION`                 | The AWS region where ECR and ECS are located.    |
| `ECR_REPOSITORY_NAME`         | Name of the ECR repository . |
| `ECS_TASK_DEFINITION_NAME`    | ECS task definition name.                        |
| `ECS_SERVICE_NAME`            | ECS service name.                                |
| `ECS_CLUSTER_NAME`            | ECS cluster name.                                |
| `AWS_ACCOUNT_ID`              | AWS Account ID where resources are hosted.       |
| `CONTAINER_IMAGE_TAG`         | Docker image tag, typically set as `${CI_COMMIT_SHORT_SHA}`. |
| `AWS_ACCESS_KEY_ID`           | AWS access key ID for authentication.            |
| `AWS_SECRET_ACCESS_KEY`       | AWS secret access key for authentication.        |

## Usage Instructions

1. **Configure the Environment Variables** in the GitLab CI/CD settings.
2. **Commit changes** to the `staging` branch to trigger the pipeline.
3. **Monitor the pipeline** in the GitLab CI/CD dashboard.
4. **Verify the deployment** in the AWS ECS console.

## Troubleshooting

- Ensure the AWS credentials have the necessary permissions.
- Check the GitLab runner logs for errors if the pipeline fails.
- Verify that the correct AWS region and account ID are used.

