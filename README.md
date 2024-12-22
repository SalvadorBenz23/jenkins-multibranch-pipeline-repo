# Jenkins Multibranch Pipeline Demo

This repository demonstrates the setup and usage of a Jenkins Multibranch Pipeline for building, testing, and deploying code across different branches. Each branch can have its own unique pipeline configuration using a Jenkinsfile.

## Purpose

The purpose of this repository is to:
	1.	Showcase the creation and management of a Multibranch Pipeline in Jenkins.
	2.	Automate builds, tests, and deployments for multiple Git branches.
	3.	Serve as a reusable guide for configuring similar pipelines in the future.

## Branches

The repository contains the following branches:
	•	main: The primary branch.
	•	dev: Development branch with build-specific steps.
	•	test: Testing branch with test-specific steps.
	•	prod: Production branch for deployment.

Each branch has its own Jenkinsfile to define branch-specific pipeline stages.

---

# Step-by-Step Setup for Jenkins Multibranch Pipeline

### 1. Repository Setup
	1.	Cloned this repository:

git clone https://github.com/SalvadorBenz23/jenkins-multibranch-pipeline-repo.git
cd jenkins-multibranch-pipeline-repo

	2.	Created branches for dev, test, and prod:

git checkout -b dev
git push --set-upstream origin dev

git checkout -b test
git push --set-upstream origin test

git checkout -b prod
git push --set-upstream origin prod

	3.	Add a unique Jenkinsfile to each branch with branch-specific pipeline stages. (See files below)

___

### 2. Jenkins Configuration

#### A. Create a Multibranch Pipeline Job
	1.	Go to your Jenkins dashboard.
	2.	Click New Item.
	3.	Choose Multibranch Pipeline and give it a name (e.g., “Multibranch Pipeline Demo”).
	4.	Click OK.

#### B. Configure the Multibranch Pipeline
	1.	Under Branch Sources:
	•	Add the GitHub repository URL:
https://github.com/SalvadorBenz23/jenkins-multibranch-pipeline-repo.git.
	•	Select credentials if needed (e.g., GitHub PAT or SSH key).
	2.	Optionally, adjust branch discovery settings:
	•	By default, Jenkins will discover all branches with a Jenkinsfile.
	3.	Save the configuration.

#### C. Scan the Pipeline
	1.	From the Multibranch Pipeline dashboard, click Scan Multibranch Pipeline Now.
	2.	Jenkins will detect all branches with a Jenkinsfile and create pipelines for them.
___

### 3. Build and Test
	1.	From the Multibranch Pipeline dashboard, select a branch (e.g., dev).
	2.	Run the pipeline and monitor the results.
	3.	Make changes to your Jenkinsfile or code, push updates to the branch, and observe the automated build process.
___

# Example Jenkinsfile

Below is an example Jenkinsfile for the dev branch:

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the dev environment...'
                sh 'echo "Build step for dev branch"'
            }
        }
        stage('Branch') {
            steps {
                echo 'Branch: dev'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed for dev.'
        }
    }
}

___

# Notes
	•	This repository serves as a template for setting up Jenkins Multibranch Pipelines.
	•	You can extend the pipelines for different environments, add more branches, or implement advanced Jenkins plugins.

Feel free to fork this repository and customise it for your needs!
