pipeline {
    agent any

    stages {
        stage('Test Emailext') {
            steps {
                script {
                    emailext(
                        to: 'darrenmccauley717@gmail.com',
                        subject: 'Test Email from Jenkins',
                        body: 'This is a test email from Jenkins using emailext.',
                        mimeType: 'text/plain'
                    )
                }
            }
        }
    }
}



