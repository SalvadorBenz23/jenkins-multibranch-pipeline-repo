pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building in the test environment...'
                // Simulate building
                sh 'echo "Build step for test branch"'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests in the test environment...'
                // Simulate testing
                sh 'echo "Test step for test branch"'
            }
        }
        stage('Branch') {
            steps {
                echo 'Branch: test'
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed for test.'
        }
    }
}
