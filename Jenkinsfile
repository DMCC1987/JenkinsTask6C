pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Your build steps here
            }
        }
        stage('Post Actions') {
            steps {
                script {
                    // Construct the path dynamically
                    def buildNumber = env.BUILD_NUMBER
                    def logFilePath = "C:\\ProgramData\\Jenkins\\.jenkins\\jobs\\GJenkinsProject\\builds\\${buildNumber}\\log"

                    try {
                        // Read the log file
                        def logContent = readFile(logFilePath)
                        
                        // Save the log file as an attachment
                        def logFile = new File("${buildNumber}_log.txt")
                        logFile.write(logContent)

                        // Send email with attachment
                        mail(
                            to: 'you@example.com',
                            subject: "Build #${buildNumber} Log",
                            body: "Please find the attached log file for build #${buildNumber}.",
                            attachmentsPattern: "${buildNumber}_log.txt"
                        )
                    } catch (Exception e) {
                        echo "Error reading or sending log file: ${e.message}"
                    }
                }
            }
        }
    }
}






