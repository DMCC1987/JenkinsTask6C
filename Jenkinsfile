pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the code from the SCM repository
                checkout scm
            }
        }

        stage('Building') {
            steps {
                echo 'Stage 1: Building the code...'
                echo 'Using Maven to compile and package the code.'
                // Add your Maven build commands here
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running unit and integration tests...'
                echo 'Using JUnit to run unit tests and pytest for integration tests.'
                // Add your test commands here
                script {
                    // Log file creation for test results
                    writeFile(file: 'unit_integration_tests.log', text: 'Unit and Integration Test results go here.')
                }
            }
            post {
                success {
                    script {
                        def logPath = "${env.WORKSPACE}/unit_integration_tests.log"
                        echo "Log file path: ${logPath}"
                        if (fileExists(logPath)) {
                            echo "Log file exists: ${logPath}"
                        }
                    }
                    // Send email notification after unit and integration tests
                    mail (
                        to: 'darrenmccauley717@gmail.com', // Replace with your email address
                        subject: "Unit and Integration Tests Successful: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        Unit and Integration Tests have completed successfully.

                        Check console output for more details: ${env.BUILD_URL}

                        Log files:
                        Unit and Integration Tests Log:
                        ${readFile('unit_integration_tests.log')}
                        """
                    )
                }
                failure {
                    // Send email notification on test failure
                    mail (
                        to: 'darrenmccauley717@gmail.com', // Replace with your email address
                        subject: "Unit and Integration Tests Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        Unit and Integration Tests have failed.

                        Check console output for more details: ${env.BUILD_URL}

                        Log files:
                        Unit and Integration Tests Log:
                        ${readFile('unit_integration_tests.log')}
                        """
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Analyzing code for quality...'
                echo 'Using SonarQube to analyze code quality and ensure industry standards.'
                // Add your SonarQube commands here
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Performing security scan...'
                echo 'Using OWASP ZAP to identify security vulnerabilities in the code.'
                script {
                    // Log file creation for security scan results
                    writeFile(file: 'security_scan.log', text: 'Security scan results go here.')
                }
            }
            post {
                success {
                    script {
                        def logPath = "${env.WORKSPACE}/security_scan.log"
                        echo "Log file path: ${logPath}"
                        if (fileExists(logPath)) {
                            echo "Log file exists: ${logPath}"
                        }
                    }
                    // Send email notification after security scan
                    mail (
                        to: 'darrenmccauley717@gmail.com', // Replace with your email address
                        subject: "Security Scan Successful: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        Security Scan has completed successfully.

                        Check console output for more details: ${env.BUILD_URL}

                        Log files:
                        Security Scan Log:
                        ${readFile('security_scan.log')}
                        """
                    )
                }
                failure {
                    // Send email notification on security scan failure
                    mail (
                        to: 'darrenmccauley717@gmail.com', // Replace with your email address
                        subject: "Security Scan Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        Security Scan has failed.

                        Check console output for more details: ${env.BUILD_URL}

                        Log files:
                        Security Scan Log:
                        ${readFile('security_scan.log')}
                        """
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploying to the staging environment...'
                echo 'Using Ansible to deploy the application to a staging server.'
                // Add your Ansible deployment commands here
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests in staging...'
                echo 'Using Selenium to run integration tests on the staging environment.'
                // Add your Selenium test commands here
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploying to the production environment...'
                echo 'Using Docker to deploy the application to the production server.'
                // Add your Docker deployment commands here
            }
        }

        stage('Debug Info') {
            steps {
                echo "Current Build Number: ${env.BUILD_NUMBER}"
                echo "Build Workspace: ${env.WORKSPACE}"
                echo "Job Name: ${env.JOB_NAME}"
                echo "Build URL: ${env.BUILD_URL}"
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}




