pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Build Android project using Gradle'
                // sh './gradlew clean assembleDebug'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Run unit tests here'
            }

            post {
                success {
                    echo 'Unit tests completed successfully'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"The status of the Unit and Integration Tests: ${currentBuild.result}",
                        body:'Log files are attached for additional information about the process',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Unit tests failed'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"The status of the Unit and Integration Tests: ${currentBuild.result}",
                        body:'Log files are attached for additional information about the process',
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Integrate code analysis tool (e.g., SonarQube)'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Perform security scan using a tool like OWASP Dependency-Check'
            }

            post {
                success {
                    echo 'Security Scan completed successfully'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"The status of the Security Scan: ${currentBuild.result}",
                        body:'Log files are attached for additional information about the process',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Security Scan failed'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"The status of the Security Scan: ${currentBuild.result}",
                        body:'Log files are attached for additional information about the process',
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploy the application to a staging server (e.g., AWS)'
                // Implement deployment commands here
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on the staging environment'
                // Implement staging integration test commands here
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploy the application to a production server (e.g., AWS)'
                // Implement production deployment commands here
            }
        }
    }
}
