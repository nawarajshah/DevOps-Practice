pipeline {
    agent any

    tools {
        nodejs 'NodeJS'
        docker 'Docker'
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
                    def dockerImage = docker.build('react-quiz-app', '-f React-Quiz-App-main/Dockerfile .')

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
                docker.image('react-quiz-app').stop()
                docker.image('react-quiz-app').remove()
            }
        }
    }
}
