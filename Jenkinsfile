pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool - Maven to compile and package the code."
                script {
                    // Simulate generating a log file (replace this with your actual log generation logic)
                    writeFile file: 'existing-log.txt', text: 'This is a sample log file.'
                }
            }
            post {
                success {
                    script {
                        // Archive the existing log file so it can be used as an attachment
                        archiveArtifacts artifacts: 'existing-log.txt', allowEmptyArchive: true
                    }
                    script {
                        try {
                            // Send email with the existing log file attached
                            emailext(
                                to: "nkongebryan44@gmail.com",
                                subject: "Build Status",
                                body: """The build status was a success!
                                       
                                        Please find the attached log file.""",
                                attachmentsPattern: 'existing-log.txt',
                                attachLog: true
                            )
                        } catch (Exception e) {
                            echo "Error sending email: ${e.getMessage()}"
                            e.printStackTrace()
                        }
                    }
                }
                failure {
                    script {
                        // Archive the existing log file so it can be used as an attachment
                        archiveArtifacts artifacts: 'existing-log.txt', allowEmptyArchive: true
                    }
                    script {
                        try {
                            emailext(
                                to: "nkongebryan44@gmail.com",
                                subject: "Build Failed",
                                body: """The build failed. Please check the attached log for details.""",
                                attachmentsPattern: 'existing-log.txt',
                                attachLog: true
                            )
                        } catch (Exception e) {
                            echo "Error sending email: ${e.getMessage()}"
                            e.printStackTrace()
                        }
                    }
                }
            }
        }
    }
}
