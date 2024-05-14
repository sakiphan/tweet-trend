
```markdown
# Jenkins Pipeline Operations

This document explains the Jenkins pipeline operations for the `main` and `dev` branches.

## Pipeline Configuration

Below is the pipeline configuration used in the Jenkinsfile:

```markdown
pipeline {
    agent {
        label 'maven'
    }

    environment {
        PATH = "/opt/apache-maven-3.9.2/bin:$PATH"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
    }
}
```

## Branch-Specific Jenkins Operations

This pipeline is configured for the `main` and `dev` branches. The pipeline runs on a specific node (`label 'maven'`) and uses the Maven build tool.

- **Checkout SCM**: The pipeline checks out the source code from the specified branch.
- **Build**: The checked-out source code is built and deployed using Maven.

## Webhook Trigger

You can use the following webhook URL to trigger the pipeline:

```markdown
http://34.207.181.38:8080/multibranch-webhook-trigger/invoke?token=devops-key
```

This URL is used to trigger the multibranch pipeline on Jenkins.

## Jenkinsfile Configuration Steps

### Pipeline Agent and Environment Variables

- The pipeline runs on a node labeled `maven`.
- The directory where Maven is installed is added to the PATH.

### Checkout SCM Stage

- Checks out the source code from the specified branch.

### Build Stage

- Uses the `mvn clean deploy` command to build and deploy the project.

## Usage Instructions

### Create Jenkinsfile

- Create a `Jenkinsfile` in the root directory of your project with the content above.

### Webhook Configuration

- Configure the webhook URL on GitHub or GitLab to trigger on commits and pull requests.
- URL: `http://34.207.181.38:8080/multibranch-webhook-trigger/invoke?token=devops-key`

### Running the Pipeline

- Create and configure a multibranch pipeline for your project in Jenkins.
- The pipeline will automatically trigger on code changes and commits.

## Notes

- Ensure that the `maven` label is correctly set up on Jenkins nodes.
- Check the directory where Maven is installed and the PATH settings.
- Use the webhook URL to trigger your Jenkins pipeline.

## Troubleshooting

- If the pipeline fails, check the error messages in the Jenkins logs.
- Review the PATH and Maven settings.
- Ensure the `Jenkinsfile` is correctly configured.

This document will help you configure the Jenkins pipeline operations for the `main` and `dev` branches. If you encounter any issues, check the Jenkins logs and configuration settings.

