pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Add your build steps here
            }
        }
    }

    post {
        success {
            echo 'Pipeline successful!'
            // Add actions for a successful build
        }
        failure {
            echo 'Pipeline failed!'
            // Add actions for a failed build
        }
    }
}
