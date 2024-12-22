pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the main environment...'
                // Simulate building
                sh 'echo "Build step for main branch"'
            }
        }
        stage('Branch') {
            steps {
                echo 'Branch: main'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed for main.'
        }
    }
}
