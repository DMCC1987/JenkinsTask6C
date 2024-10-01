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
                sh 'mvn clean package > build.log' // Log the build output
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Stage 2: Running unit and integration tests...'
                    echo 'Using JUnit to run unit tests and pytest for integration tests.'
                    // Replace this line with the actual command to run your tests and generate logs
                    sh 'mvn test > unit_integration_tests.log' // Log the unit/integration test output
                }
            }
            post {
                success {
                    script {
                        def logFilePath = "${env.WORKSPACE}/unit_integration_tests.log"
                        sendNotificationEmail("Unit and Integration Tests Success: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, true)
                    }
                }
                failure {
                    script {
                        def logFilePath = "${env.WORKSPACE}/unit_integration_tests.log"
                        sendNotificationEmail("Unit and Integration Tests Failed: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, false)
                    }
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code for quality...'
                echo 'Using SonarQube to analyze code quality and ensure industry standards.'
                // Add your SonarQube command here
                sh 'sonar-scanner > code_analysis.log' // Log the SonarQube analysis output
            }
            post {
                success {
                    script {
                        def logFilePath = "${env.WORKSPACE}/code_analysis.log"
                        sendNotificationEmail("Code Analysis Success: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, true)
                    }
                }
                failure {
                    script {
                        def logFilePath = "${env.WORKSPACE}/code_analysis.log"
                        sendNotificationEmail("Code Analysis Failed: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, false)
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                echo 'Using OWASP ZAP to identify security vulnerabilities in the code.'
                // Add your security scan command here
                sh 'zap.sh -quick -o security_scan.log' // Log the security scan output
            }
            post {
                success {
                    script {
                        def logFilePath = "${env.WORKSPACE}/security_scan.log"
                        sendNotificationEmail("Security Scan Success: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, true)
                    }
                }
                failure {
                    script {
                        def logFilePath = "${env.WORKSPACE}/security_scan.log"
                        sendNotificationEmail("Security Scan Failed: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, false)
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                echo 'Using Ansible to deploy the application to a staging server.'
                // Add your deployment command here
                sh 'ansible-playbook deploy_staging.yml > deploy_staging.log' // Log the staging deployment output
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests in staging...'
                echo 'Using Selenium to run integration tests on the staging environment.'
                // Add your integration test command here
                sh 'pytest integration_tests.py > integration_tests_staging.log' // Log the integration test output
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                echo 'Using Docker to deploy the application to the production server.'
                // Add your production deployment command here
                sh 'docker-compose up -d > deploy_production.log' // Log the production deployment output
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

// Function to send notification email
def sendNotificationEmail(String subject, String logFilePath, boolean success) {
    echo "Log file path: ${logFilePath}"
    if (fileExists(logFilePath)) {
        echo "Log file exists: ${logFilePath}"
    } else {
        echo "Log file does not exist: ${logFilePath}"
    }

    // Log the subject and body before sending
    String emailSubject = subject
    String emailBody = """The stage ${success ? 'was successful' : 'failed'}. 

Check console output for more details: ${env.BUILD_URL}"""

    echo "Subject: ${emailSubject}"
    echo "Body: ${emailBody}"

    // Send email with attachment using PowerShell
    powershell """
    $emailFrom = 'you@example.com'
    $emailTo = 'recipient@example.com'
    $subject = '${emailSubject}'
    $body = @"
    ${emailBody}
    "@
    $smtpServer = 'smtp.example.com'
    $attachment = '${logFilePath}'
    
    $message = New-Object System.Net.Mail.MailMessage
    $message.From = $emailFrom
    $message.To.Add($emailTo)
    $message.Subject = $subject
    $message.Body = $body
    if (Test-Path $attachment) {
        $message.Attachments.Add($attachment)
    }

    $smtp = New-Object Net.Mail.SmtpClient($smtpServer)
    $smtp.Send($message)
    """
}







