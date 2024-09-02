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
                        // Check if the file exists
                        if (fileExists(logFilePath)) {
                            // Read the log file
                            def logContent = readFile(logFilePath)
                            
                            // Save the log file as an artifact
                            writeFile file: "build_${buildNumber}_log.txt", text: logContent

                            // Archive the log file as an artifact
                            archiveArtifacts artifacts: "build_${buildNumber}_log.txt", onlyIfSuccessful: true

                            // Send email with attachment
                            mail(
                                to: 'you@example.com',
                                subject: "Build #${buildNumber} Log",
                                body: "Please find the attached log file for build #${buildNumber}.",
                                attachmentsPattern: "build_${buildNumber}_log.txt"
                            )
                        } else {
                            echo "Log file does not exist at path: ${logFilePath}"
                        }
                    } catch (Exception e) {
                        echo "Error reading or sending log file: ${e.message}"
                    }
                }
            }
        }
    }
}






