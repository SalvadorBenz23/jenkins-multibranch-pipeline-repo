pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the dev environment...'
                sh 'echo "Build step for dev branch"'
            }
        }
        stage('Test Webhook') {
            steps {
                echo 'Testing webhook for dev branch...'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed for dev.'
        }
    }
}
