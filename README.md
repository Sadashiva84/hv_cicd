# hv_cicd

# 1. Jenkins CI/CD Pipeline for Flask Application

## Objective

Set up a Jenkins pipeline to automate the testing and deployment of a simple Python web application.

## Requirements

### 1. Setup:

- Install Jenkins on a virtual machine or use a cloud-based Jenkins service.
- Configure Jenkins with Python and any necessary libraries.

### 2. Source Code:

- Fork the provided Python web application repository on [GitHub](https://github.com/Sadashiva84/hv_cicd).
- Clone the forked repository into your Jenkins server.

### 3. Jenkins Pipeline:

- Create a `Jenkinsfile` in the root of your Python application repository.
- Define a pipeline with the following stages:
  - **Build:** Install dependencies using pip.
  - **Test:** Run unit tests using a testing framework like pytest.
  - **Deploy:** If tests pass, deploy the application to a staging environment.
 
'''

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Install dependencies using pip
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run unit tests using pytest
                    sh 'pytest'
                }
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                script {
                    // Deploy to staging environment (replace with your deployment script)
                    sh './deploy-to-staging.sh'
                }
            }
        }
    }

    post {
        always {
            // Clean up or perform any post-build actions here
        }
    }
}

'''

### 4. Triggers:

- Configure the pipeline to trigger a new build whenever changes are pushed to the main branch of the repository.

### 5. Notifications:

- Set up a notification system to alert via email when the build process fails or succeeds.

### 6. Documentation:

- Document the pipeline process and any prerequisites needed for the setup in a `README.md` file in the repository.

### 7. Submission:

- The URL to the [GitHub repository](provide-repo-url) with the `Jenkinsfile` and updated `README.md`.
- Include screenshots of the Jenkins pipeline showing the build, test, and deployment stages.


# 2. GitHub Actions CI/CD Pipeline for Flask App

## Objective

Implement a CI/CD workflow using GitHub Actions for a Python application.

## Requirements

### 1. Setup:

- Use a provided Python application repository on [GitHub](https://github.com/Sadashiva84/hv_cicd).
- Ensure the repository has a `main` branch and a `staging` branch.

### 2. GitHub Actions Workflow:

- Create a `.github/workflows` directory in your repository.
- Inside the directory, create a YAML file to define the workflow.

### 3. Workflow Steps:

- Define a workflow that performs the following jobs:
  - **Install Dependencies:** Install all necessary dependencies for the Python application using pip.
  - **Run Tests:** Execute the test suite using a framework like pytest.
  - **Build:** If tests pass, prepare the application for deployment.
  - **Deploy to Staging:** Deploy the application to a staging environment when changes are pushed to the `staging` branch.
  - **Deploy to Production:** Deploy the application to production when a release is tagged.

### 4. Environment Secrets:

- Use GitHub Secrets to store sensitive information required for deployments (e.g., deployment keys, API tokens).

### 5. Documentation:

- Update the `README.md` file with instructions on how the GitHub Actions workflow works and how to configure the necessary secrets.

### 6. Submission:

- The URL to the [GitHub repository](provide-repo-url) with the workflow file and updated `README.md`.
- Include screenshots of the GitHub Actions workflow runs showing successful execution of all steps.

