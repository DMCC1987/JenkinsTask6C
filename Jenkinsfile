pipeline {
    agent any
    stages {
        stage('Building') {
            steps {
                echo 'Stage 1: Building the code...'
                echo 'Using Maven to compile and package the code.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                echo 'Using JUnit to run unit tests and pytest for integration tests.'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code for quality...'
                echo 'Using SonarQube to analyze code quality and ensure industry standards.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                echo 'Using OWASP ZAP to identify security vulnerabilities in the code.'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                echo 'Using Ansible to deploy the application to a staging server.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests in staging...'
                echo 'Using Selenium to run integration tests on the staging environment.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                echo 'Using Docker to deploy the application to the production server.'
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
                echo 'Pipeline succeeded!'
                def logFile = getLatestLogFile()
                try {
                    sendEmail("Build Success: ${env.JOB_NAME} - ${env.BUILD_NUMBER}", logFile, true)
                } catch (Exception e) {
                    echo "Failed to send email: ${e.message}"
                }
            }
        }
        failure {
            script {
                echo 'Pipeline failed!'
                def logFile = getLatestLogFile()
                try {
                    sendEmail("Build Failure: ${env.JOB_NAME} - ${env.BUILD_NUMBER}", logFile, false)
                } catch (Exception e) {
                    echo "Failed to send email: ${e.message}"
                }
            }
        }
    }
}

// Function to get the latest log file path
def getLatestLogFile() {
    def buildDir = "C:/ProgramData/Jenkins/.jenkins/jobs/GJenkinsProject/builds"
    def buildNumber = currentBuild.number.toString()
    def logFilePath = "${buildDir}/${buildNumber}/log"

    if (fileExists(logFilePath)) {
        echo "Log file found: ${logFilePath}"
        return logFilePath
    } else {
        echo "Log file not found: ${logFilePath}"
        error("Log file not found: ${logFilePath}")
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

    // Send email with attachment
    emailext(
        to: 'darrenmccauley717@gmail.com',
        subject: subject,
        body: """The build ${success ? 'was successful' : 'failed'}. 

Check console output for more details: ${env.BUILD_URL}""",
        attachmentsPattern: logFilePath,
        mimeType: 'text/plain'
    )
}








