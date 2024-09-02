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
    }
    post {
        always {
            script {
                def logFile = "${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log"
                def psScript = "C:\\path\\to\\send-email.ps1"
                def command = "powershell -File ${psScript} -SmtpServer 'smtp.gmail.com' -SmtpPort 587 -SmtpFrom 'darrenmccauley717@gmail.com' -SmtpTo 'darrenmccauley717@gmail.com' -Subject 'Build Report: ${env.JOB_NAME} - ${env.BUILD_NUMBER}' -Body 'Build log attached.' -AttachmentPath '${logFile}' -SmtpUser 'darrenmccauley717@gmail.com' -SmtpPassword 'YOUR_APP_PASSWORD'"
                
                bat script: command
            }
        }
    }
}






