pipeline {
    agent any

    tools {
        // Use the correct tool names configured in Jenkins for Node.js and Docker
        nodejs 'NodeJS'
        dockerTool 'Docker'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Build the Docker image
                    def dockerImage = dockerTool build('-f React-Quiz-App-main/Dockerfile .')

                    // Run the Docker container
                    dockerImage.run('-p 8080:80 --name react-quiz-app-container')

                    // Optional: You can add additional deployment steps here
                    // For example, deploy to Kubernetes, notify external systems, etc.
                }
            }
        }
    }

    post {
        success {
            // Actions to perform if the pipeline is successful
            echo 'Pipeline successful!'
        }

        failure {
            // Actions to perform if the pipeline fails
            echo 'Pipeline failed!'
        }

        always {
            // Cleanup steps (e.g., stop and remove Docker containers)
            script {
                dockerTool.image('react-quiz-app').stop()
                dockerTool.image('react-quiz-app').remove()
            }
        }
    }
}
