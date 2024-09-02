pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add a basic build step, like printing a message
            }
        }
    }

    post {
        always {
            // Email notification step
            emailext(
                to: 'darrenmccauley717@gmail.com',
                subject: 'Jenkins Job: ${JOB_NAME} - Build #${BUILD_NUMBER} - ${BUILD_STATUS}',
                body: "Check console output at ${BUILD_URL} to view the results."
            )
        }
    }
}



