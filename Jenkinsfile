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
                def recipient = 'darrenmccauley717@gmail.com'
                def subject = "Build ${currentBuild.result}: ${env.JOB_NAME} - ${env.BUILD_NUMBER}"
                def body = "The build ${currentBuild.result.toLowerCase()}.\n\nCheck the attached log file for details.\n\n${env.BUILD_URL}"
                
                bat """
                powershell -Command \\
                $smtpServer = "smtp.gmail.com"; \\
                $smtpPort = 587; \\
                $smtpFrom = "darrenmccauley717@gmail.com"; \\
                $smtpTo = "${recipient}"; \\
                $messageSubject = "${subject}"; \\
                $messageBody = "${body}"; \\
                $attachment = "${logFile}"; \\
                $smtpUser = "darrenmccauley717@gmail.com"; \\
                $smtpPassword = "YOUR_APP_PASSWORD"; \\
                $smtp = New-Object Net.Mail.SmtpClient($smtpServer, $smtpPort); \\
                $smtp.EnableSsl = $true; \\
                $smtp.Credentials = New-Object System.Net.NetworkCredential($smtpUser, $smtpPassword); \\
                $message = New-Object Net.Mail.MailMessage($smtpFrom, $smtpTo, $messageSubject, $messageBody); \\
                $attachment = New-Object Net.Mail.Attachment($attachment); \\
                $message.Attachments.Add($attachment); \\
                $smtp.Send($message);
                """
            }
        }
    }
}





