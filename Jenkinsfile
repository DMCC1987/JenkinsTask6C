stage('Send Email Notification') {
    steps {
        script {
            emailext (
                to: 'darrenmccauley717@gmail.com', // Your email
                subject: "Test Email from Jenkins",
                body: """
                This is a test email sent from Jenkins.
                Check the log file for details.

                Log files:
                Unit and Integration Tests Log:
                ${readFile('unit_integration_tests.log')}
                """,
                attachLog: true // Attach the console log
            )
        }
    }
}






