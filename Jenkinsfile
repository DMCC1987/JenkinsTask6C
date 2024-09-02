pipeline {
    agent any
    stages {
        stage('Test Emailext') {
            steps {
                script {
                    emailext(
                        to: 'your-email@example.com',  // Replace with your test email address
                        subject: 'Test Email from Jenkins',
                        body: 'This is a test email from Jenkins using emailext.',
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }
}


