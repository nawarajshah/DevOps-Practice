pipeline {
    agent any

    environment {
        // Define the Node.js installation in the environment
        NODEJS_HOME = tool 'NodeJS'
        PATH = "$NODEJS_HOME/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Install npm dependencies
                sh 'npm install'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Run tests using npm
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment commands here
            }
        }
    }

    post {
        failure {
            // This block will be executed if any of the stages fail
            echo 'One or more stages failed. Take necessary actions.'
        }
    }
}
