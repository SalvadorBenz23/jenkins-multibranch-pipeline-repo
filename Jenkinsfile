pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the dev environment...'
                // Simulate building
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
