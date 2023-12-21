pipeline {
    agent any
    tools {
        nodejs "NodeJS 21"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Replace with your deployment commands
            }
        }
    }
}
