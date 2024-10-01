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
        success {
            script {
                echo 'Pipeline succeeded!'
                // Finding the most recent log file dynamically
                def logFile = findLogFile()
                // Sending email on success
                emailext(
                    to: 'darrenmccauley717@gmail.com',
                    subject: "Build Success: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                    body: """The build was successful!

Check console output for more details: ${env.BUILD_URL}""",
                    attachmentsPattern: logFile,
                    mimeType: 'text/plain'
                )
            }
        }
        failure {
            script {
                echo 'Pipeline failed!'
                // Finding the most recent log file dynamically
                def logFile = findLogFile()
                // Sending email on failure
                emailext(
                    to: 'darrenmccauley717@gmail.com',
                    subject: "Build Failure: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                    body: """The build failed.

Check console output for more details: ${env.BUILD_URL}""",
                    attachmentsPattern: logFile,
                    mimeType: 'text/plain'
                )
            }
        }
    }
}

// Function to find the most recent log file dynamically
def findLogFile() {
    def buildDir = "C:/ProgramData/Jenkins/.jenkins/jobs/GJenkinsProject/builds"
    def buildNumber = currentBuild.number.toString()
    return "${buildDir}/${buildNumber}/log"
}









