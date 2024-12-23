# Jenkins Multibranch Pipeline Demo

This repository demonstrates the setup and usage of a Jenkins Multibranch Pipeline for building, testing, and deploying code across different branches. Each branch can have its own unique pipeline configuration using a Jenkinsfile. It also showcases the use of webhooks for triggering builds automatically on code changes (on push).

**CI/CD EDIT:**
Forgot to mention the main/master branch used as the default branch (could be configured to be prod). The main branch is here to act as a merging point from dev or test **while Webhooks allows us to test our automated deployment in each branch** before any stable version is released to main.

**GitHub flow**

![image](https://github.com/user-attachments/assets/3841965f-ea28-4456-a3cd-505fae9847d6)

**Pull request Workflow**
![image](https://github.com/user-attachments/assets/f3ad4eab-a2c6-427a-a129-2d30801675e4)

Git flow (not applied for this simple project)
![image](https://github.com/user-attachments/assets/38bd79c5-1018-43cc-81db-5f52674b448a)


---

## Purpose

The purpose of this repository is to:

1. Showcase the creation and management of a Multibranch Pipeline in Jenkins.
2. Automate builds, tests, and deployments for multiple Git branches.
3. Create a webhook for automated build triggers on code changes.
4. Serve as a reusable guide for configuring similar pipelines in the future.
   
---

## Branches

The repository contains the following branches:

- **main**: The primary branch.
- **dev**: Development branch with build-specific steps.
- **test**: Testing branch with test-specific steps.
- **prod**: Production branch for deployment.

Each branch has its own Jenkinsfile to define branch-specific pipeline stages.

---

## Step-by-Step Setup for Jenkins Multibranch Pipeline

### 1. Repository Setup

1. Cloned this repository:
   ```bash
   git clone https://github.com/SalvadorBenz23/jenkins-multibranch-pipeline-repo.git
   cd jenkins-multibranch-pipeline-repo
   ```
   
2. Create branches for dev, test, and prod:
   ```bash
   git checkout -b dev
   git push --set-upstream origin dev

   git checkout -b test
   git push --set-upstream origin test

   git checkout -b prod
   git push --set-upstream origin prod
   ```

3. Added a unique Jenkinsfile to each branch with branch-specific pipeline stages. (See files below)

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

```Groovy
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
```
___

# 3. Webhook Setup for Automated Builds

#### A. Create a GitHub Personal Access Token (PAT)
1. Go to GitHub Settings → Developer Settings → Personal Access Tokens → Tokens (Classic).
2. Generate a new token with the following scopes:
	•	repo: For accessing private/public repositories.
	•	admin:repo_hook: For managing webhooks.
3. Save the token securely (it will only be shown once).

#### B. Add Jenkins Credentials
1. In Jenkins, go to Manage Jenkins → Manage Credentials.
2. Add a Secret Text credential with:
	•	Scope: Global.
	•	Secret: Paste the PAT.
	•	ID: github-webhook.

#### C. Configure a Webhook in GitHub
1. Go to your GitHub repository → Settings → Webhooks → Add Webhook.
2. Set the following:
	•	Payload URL: http://<JENKINS_PUBLIC_IP>:8080/github-webhook/.
	•	Content Type: application/json.
	•	Trigger: Check Push events.
3. Save the webhook.

#### D. Enable Webhooks in Jenkins
1. Go to the Multibranch Pipeline configuration.
2. In the Build Triggers section, select GitHub hook trigger for GITScm polling.
3. Save the configuration.

#### E. Test the Webhook
1. Make a change to any branch (e.g., dev) and push the changes:

   ```bash
   git add .
   git commit -m "Test webhook"
   git push origin dev
   ```
2. Verify that the webhook triggers a build in Jenkins. (limited API call when not running HTTPS, might take a while to validate but works)
   
___
# Notes
	• This repository serves as a template for setting up Jenkins Multibranch Pipelines.
	• You can extend the pipelines for different environments, add more branches, or implement advanced Jenkins plugins.

- **Periodic Builds**:  
  Jenkins can schedule builds automatically using Cron syntax:  
  - Navigate to **Build Triggers**.  
  - Select **Build periodically** and specify the schedule.  
    Example: `* * * * *` runs the pipeline every minute.

- **GitHub API Quota**:  
  Using Jenkins anonymously limits GitHub API requests. Authenticate Jenkins with a Personal Access Token (PAT) to increase the quota to 5000 requests per hour.

- **IP Package**:  
  An IP address package (`iproute2`) was initially considered but wasn’t required for this setup.

Feel free to fork and customize this repository for your projects!

Feel free to fork this repository and customise it for your needs!
