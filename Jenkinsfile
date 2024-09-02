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
            echo 'Pipeline succeeded!'
            script {
                def buildLog = "${env.WORKSPACE}/builds/${env.BUILD_NUMBER}/log"
                emailext (
                    to: 'darrenmccauley717@gmail.com',
                    subject: "Build Success: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                    body: """\
                        The build was successful!

                        Check console output for more details: ${env.BUILD_URL}
                    """,
                    attachLog: true
                )
            }
        }
        failure {
            echo 'Pipeline failed!'
            script {
                def buildLog = "${env.WORKSPACE}/builds/${env.BUILD_NUMBER}/log"
                emailext (
                    to: 'darrenmccauley717@gmail.com',
                    subject: "Build Failure: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                    body: """\
                        The build failed.

                        Check console output for more details: ${env.BUILD_URL}
                    """,
                    attachLog: true
                )
            }
        }
    }
}






