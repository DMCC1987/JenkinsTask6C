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
                    def buildNumber = env.BUILD_NUMBER
                    def logFilePath = "C:\\ProgramData\\Jenkins\\.jenkins\\jobs\\GJenkinsProject\\builds\\${buildNumber}\\log"

                    try {
                        if (fileExists(logFilePath)) {
                            def logContent = readFile(logFilePath)
                            writeFile file: "build_${buildNumber}_log.txt", text: logContent
                            archiveArtifacts artifacts: "build_${buildNumber}_log.txt", onlyIfSuccessful: true
                            
                            emailext (
                                to: 'darrenmccauley717@gmail.com',
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







