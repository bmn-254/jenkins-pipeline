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
                    mail to: "nkongebryan44@gmail.com",
                         subject: "Build Status",
                         body: "The build status was a success. Please find the attached build log.",
                         attachmentsPattern: 'build-log.txt'
                }
            }
        } // Close stage('Build')

        stage('Unit and Integration Tests') {
            steps { 
                echo "Use test automation tool - JUnit for unit tests and integration test purposes."
            }
        } // Close stage('Unit and Integration Tests')

        stage('Code Analysis') {
            steps { 
                echo "Integrate a code analysis tool - SonarQube."
            }
        } // Close stage('Code Analysis')

        stage('Security Scan') {
            steps { 
                echo "Perform a security scan using a tool - OWASP ZAP."
            }
        } // Close stage('Security Scan')

        stage('Deploy to Staging') {
            steps { 
                echo "Deploy the application to a staging server using deployment tool - Docker."
            }
        } // Close stage('Deploy to Staging')

        stage('Integration Tests on Staging') {
            steps { 
                echo "Run integration tests on the staging environment."
            }
        } // Close stage('Integration Tests on Staging')

        stage('Deploy to Production') {
            steps { 
                echo "Deploy the application to a production server using deployment tool - Docker."
            }
        } // Close stage('Deploy to Production')
    } // Close stages
} // Close pipeline
