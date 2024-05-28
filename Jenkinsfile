pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool - Maven to compile and package the code."
                script {
                    // Capture the build log
                    def log = currentBuild.rawBuild.getLog().join("\n")
                    // Write the log to a file
                    writeFile file: 'build-log.txt', text: log
                }
            }
            post {
                success {
                    script {
                        // Archive the log file so it can be used as an attachment
                        archiveArtifacts artifacts: 'build-log.txt', allowEmptyArchive: true
                    }
                    // Send email with the log file attached
                    emailext(
                        to: "nkongebryan44@gmail.com",
                        subject: "Build Status",
                        body: """The build status was a success!
                                 
                                 Please find the attached build log.""",
                        attachLog: true,
                        attachmentsPattern: 'build-log.txt'
                    )
                }
                failure {
                    script {
                        // Capture the build log
                        def log = currentBuild.rawBuild.getLog().join("\n")
                        // Write the log to a file
                        writeFile file: 'build-log.txt', text: log
                        // Archive the log file so it can be used as an attachment
                        archiveArtifacts artifacts: 'build-log.txt', allowEmptyArchive: true
                    }
                    emailext(
                        to: "nkongebryan44@gmail.com",
                        subject: "Build Failed",
                        body: """The build failed. Please check the attached log for details.""",
                        attachLog: true,
                        attachmentsPattern: 'build-log.txt'
                    )
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Use test automation tool - JUnit for unit tests and integration test purposes."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrate a code analysis tool - SonarQube."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Perform a security scan using a tool - OWASP ZAP."
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging server using deployment tool - Docker."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment."
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy the application to a production server using deployment tool - Docker."
            }
        }
    }
}
