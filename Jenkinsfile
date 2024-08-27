pipeline {
    agent any
    stages {
        stage('Send Test Emails') {
            steps {
                echo 'Executing the pipeline stages...'
                // Include any other steps needed for your pipeline here
            }
        }
    }
    post {
        success {
            echo 'Pipeline succeeded!'
            mail to: 'darrenmccauley717@gmail.com',
                 subject: "Test Email",
                 body: "This is a test email to verify email configuration."
        }
        failure {
            echo 'Pipeline failed!'
            mail to: 'darrenmccauley717@gmail.com',
                 subject: "Build Failure: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                 body: "The build failed.\n\n" +
                       "Check console output for more details: ${env.BUILD_URL}"
        }
    }
}
