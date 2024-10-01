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
                echo 'Using Maven to compile and package the code.'
                // Add your Maven build command here
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                echo 'Using JUnit to run unit tests and pytest for integration tests.'
                // Add your test commands here
            }
            post {
                success {
                    script {
                        sendNotificationEmail("Unit and Integration Tests Success: ${env.JOB_NAME} - ${currentBuild.number}", true)
                    }
                }
                failure {
                    script {
                        sendNotificationEmail("Unit and Integration Tests Failed: ${env.JOB_NAME} - ${currentBuild.number}", false)
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code for quality...'
                echo 'Using SonarQube to analyze code quality and ensure industry standards.'
                // Add your SonarQube command here
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                echo 'Using OWASP ZAP to identify security vulnerabilities in the code.'
                // Add your security scan command here
            }
            post {
                success {
                    script {
                        sendNotificationEmail("Security Scan Success: ${env.JOB_NAME} - ${currentBuild.number}", true)
                    }
                }
                failure {
                    script {
                        sendNotificationEmail("Security Scan Failed: ${env.JOB_NAME} - ${currentBuild.number}", false)
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                echo 'Using Ansible to deploy the application to a staging server.'
                // Add your deployment command here
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests in staging...'
                echo 'Using Selenium to run integration tests on the staging environment.'
                // Add your integration test command here
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                echo 'Using Docker to deploy the application to the production server.'
                // Add your production deployment command here
            }
        }

        stage('Debug Info') {
            steps {
                script {
                    echo "Current Build Number: ${currentBuild.number}"
                    echo "Build Workspace: ${env.WORKSPACE}"
                    echo "Job Name: ${env.JOB_NAME}"
                    echo "Build URL: ${env.BUILD_URL}"
                }
            }
        }
    }

    post {
        success {
            script {
                echo "Pipeline completed successfully."
            }
        }
        failure {
            script {
                echo "Pipeline failed."
            }
        }
    }
}

// Function to send notification email with log attachment
def sendNotificationEmail(String subject, boolean success) {
    // Define log file path
    def logFilePath = "${env.WORKSPACE}/builds/${currentBuild.number}/log" // Update this path as needed

    String emailSubject = subject
    String emailBody = """The stage ${success ? 'was successful' : 'failed'}. 

Check console output for more details: ${env.BUILD_URL}"""

    // Log email details before sending
    echo "Subject: ${emailSubject}"
    echo "Body: ${emailBody}"

    // Check if log file exists
    if (fileExists(logFilePath)) {
        echo "Log file exists: ${logFilePath}"
        
        // Send email with attachment (implementation not executed)
        mail to: 'recipient@example.com',
             subject: emailSubject,
             body: emailBody,
             attachments: [logFilePath] // This line would send the attachment
    } else {
        echo "Log file does not exist: ${logFilePath}"
        
        // Send email without attachment
        mail to: 'recipient@example.com',
             subject: emailSubject,
             body: emailBody
    }
}








