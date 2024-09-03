pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
    post {
        always {
            script {
                // Simple test to send an email
                emailext(
                    to: 'youremail@example.com',
                    subject: 'Jenkins Test Email',
                    body: 'This is a simple test email from Jenkins.'
                )
            }
        }
    }
}








