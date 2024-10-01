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
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to the staging environment...'
                // Your deployment commands here (e.g., Ansible)
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in staging...'
                // Your integration test commands here (e.g., Selenium)
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to the production environment...'
                // Your production deployment commands here (e.g., Docker)
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

                // Send email with log information
                mail to: 'darrenmccauley717@gmail.com',
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


