pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'This is a test build for GitHub and Jenkins'
                // sh './GitHub/Jenkins'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'This stage is used to run tests'
            }

            post {
                success {
                    echo 'The tests were completed successfully'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"Unit and Integration Tests Status: ${currentBuild.result}",
                        body:'Kindly find attached the log files with more information',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Unit tests were not successful'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"Unit and Integration Tests Status: ${currentBuild.result}",
                        body:'Kindly find attached the log files with more information',
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
                echo 'Perform security scan using OWASP Dependency-Check'
            }

            post {
                success {
                    echo 'Security Scan was a success'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"Security Satus: ${currentBuild.result}",
                        body:'Kindly find attached the log files with more information',
                        attachLog: true
                    )
                }
                failure {
                    echo 'Security Scan were not successful'
                    emailext(
                        to: 'nkongebryan44@gmail.com',
                        subject:"Security Scan Status: ${currentBuild.result}",
                        body:'Kindly find attached the log files with more information',
                        attachLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploy the application to a staging server (like AWS)'
                // Deployment of Implementation commands
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on the staging environment'
                // Deployment of Staging Integration tests
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploy the application to a production server (e.g., AWS)'
                // Deployment of Production Deployment commands
            }
        }
    }
}
