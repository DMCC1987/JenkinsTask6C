pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Building') {
            steps {
                echo 'Stage 1: Building the code...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                script {
                    // Create a log file for demonstration
                    writeFile(file: 'unit_integration_tests.log', text: 'Unit and Integration Test results go here.')
                }
            }
        }

        stage('Send Email Notification') {
            steps {
                script {
                    emailext (
                        to: 'darrenmccauley717@gmail.com', // Your email
                        subject: "Test Email from Jenkins",
                        body: """
                        This is a test email sent from Jenkins.
                        Check the log file for details.

                        Log files:
                        Unit and Integration Tests Log:
                        ${readFile('unit_integration_tests.log')}
                        """,
                        attachments: 'unit_integration_tests.log', // Ensure this file exists
                        smtpCredentialsId: '9c59c3f5-3272-43ea-97f3-f9dcfe9122e9', // Your credential ID
                        attachLog: true // Attach the console log
                    )
                }
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}






