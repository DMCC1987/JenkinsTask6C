pipeline {
    agent any
    stages {
        stage('Send Test Emails') {
            steps{
                echo 'Sending a test email to verify email configuration...'
            }
            post{
                success{
                    mail to: 'darrenmccauley717@gmail.com',
                    subject: "Test Email",
                    body: "This is a test email to verify email configuration."
                }
            }
        }
