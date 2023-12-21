pipeline {
    agent any

    tools {
        // Define the Maven tool installation
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the Maven project
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run Maven test phase
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // You can add deployment steps here
                echo 'Deploying...'
            }
        }
    }

    post {
        success {
            // Actions to perform if the build is successful
            echo 'Build successful!'

            // You can add additional post-build actions here
        }

        failure {
            // Actions to perform if the build fails
            echo 'Build failed!'
        }

        always {
            // Actions to perform regardless of the build result
            echo 'Cleaning up...'
        }
    }
}
