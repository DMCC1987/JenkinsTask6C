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
                def logFilePath = "${env.WORKSPACE}/builds/${currentBuild.number}/log"
                sendEmail("Build Success: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, true)
            }
        }
        failure {
            script {
                def logFilePath = "${env.WORKSPACE}/builds/${currentBuild.number}/log"
                sendEmail("Build Failure: ${env.JOB_NAME} - ${currentBuild.number}", logFilePath, false)
            }
        }
    }
}

// Function to send email
def sendEmail(String subject, String logFilePath, boolean success) {
    echo "Log file path: ${logFilePath}"
    if (fileExists(logFilePath)) {
        echo "Log file exists: ${logFilePath}"
    } else {
        echo "Log file does not exist: ${logFilePath}"
    }

    // Log the subject and body before sending
    String emailSubject = subject
    String emailBody = """The build ${success ? 'was successful' : 'failed'}. 

Check console output for more details: ${env.BUILD_URL}"""

    echo "Subject: ${emailSubject}"
    echo "Body: ${emailBody}"

    // Send email with attachment
    emailext(
        to: 'darrenmccauley717@gmail.com',
        subject: emailSubject,
        body: emailBody,
        attachmentsPattern: "builds/${currentBuild.number}/log", // Adjusted to the correct path
        mimeType: 'text/plain'
    )
}









