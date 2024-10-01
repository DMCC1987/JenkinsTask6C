pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Your build commands here (e.g., Maven, Gradle, etc.)
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Your test commands here
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code for quality...'
                // Your code analysis commands here (e.g., SonarQube)
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Your security scan commands here (e.g., OWASP ZAP)
            }
        }
    }
    
    post {
        always {
            script {
                // Retrieve log files from the workspace
                def logFiles = findFiles(glob: '*.log') // Adjust the pattern if necessary
                def logContent = ''
                
                // Read each log file and append its content
                for (file in logFiles) {
                    logContent += "Log File: ${file}\n"
                    logContent += readFile(file) + "\n\n"
                }

                // Send email with log information after tests and security scan
                mail to: 'recipient@example.com',
                     subject: "Build Logs for Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: """
                     <p>Please find the log information below:</p>
                     <pre>${logContent}</pre>
                     """,
                     mimeType: 'text/html'
            }
        }
    }
}


