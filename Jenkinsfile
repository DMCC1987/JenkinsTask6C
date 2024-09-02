pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Simulate build step here
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Simulate test step here
            }
        }
    }
    post {
        always {
            script {
                // Define the path to the build log file
                def buildNumber = env.BUILD_NUMBER.toInteger()
                def logFile = "${env.WORKSPACE}/../jobs/GJenkinsProject/builds/${buildNumber}/log"
                
                // Define the recipient email
                def recipient = 'darrenmccauley717@gmail.com'
                
                // Read the log file content
                def logContent = readFile(file: logFile)
                
                // Use the built-in mail step to send an email with the log file as an attachment
                mail to: recipient,
                     subject: "Build ${buildNumber} Log",
                     body: "Please find the build log attached.",
                     attachmentsPattern: logFile
            }
        }
    }
}







