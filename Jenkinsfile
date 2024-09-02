pipeline {
    agent any
    stages {
        stage('Building') {
            steps {
                echo 'Stage 1: Building the code...'
                // Example Maven build command
                sh 'mvn clean package'
                // Save build logs
                sh 'echo "Build logs..." > build.log'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                // Example test commands
                sh 'mvn test'
                sh 'pytest > integration-tests.log'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code for quality...'
                // Example code analysis command
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                // Example security scan command
                sh 'owasp-zap -t http://yourappurl -o security-scan-report.html'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                // Example deployment command
                sh 'ansible-playbook -i inventory/hosts deploy-staging.yml'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests in staging...'
                // Example integration tests command
                sh 'selenium-server -jar selenium-server-standalone.jar'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                // Example production deployment command
                sh 'docker-compose up -d'
            }
        }
    }
    post {
        always {
            script {
                def emailSubject = "Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}"
                def emailBody = """\
                    Build Details:
                    - Build Number: ${currentBuild.number}
                    - Status: ${currentBuild.currentResult}
                    - URL: ${env.BUILD_URL}
                    - Logs: ${env.BUILD_URL}console
                """
                // Archive logs to be attached
                archiveArtifacts artifacts: 'build.log, integration-tests.log, security-scan-report.html', allowEmptyArchive: true

                // Send email with attachments
                emailext (
                    subject: emailSubject,
                    body: emailBody,
                    attachmentsPattern: '**/*.log,**/*.html',  // Adjust the pattern to match your log files
                    to: 'darrenmccauley717@gmail.com'
                )
            }
        }
    }
}


