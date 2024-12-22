pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the production environment...'
                // Simulate building
                sh 'echo "Build step for prod branch"'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to production...'
                // Simulate deployment
                sh 'echo "Deploy step for prod branch"'
            }
        }
        stage('Branch') {
            steps {
                echo 'Branch: prod'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed for prod.'
        }
    }
}
