pipeline {
    agent any

    environment {
        // Define environment variables for email configuration
        EMAIL_RECIPIENT = 'nkongebryan44@gmail.com'
        BUILD_STATUS = 'SUCCESS'
    }

    stages {
        stage('Build') {
            steps {
                // Using Maven for build
                script {
                    try {
                        bat 'mvn clean package'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Build failed: ${e.message}"
                    }
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                // Running unit tests with JUnit and integration tests
                script {
                    try {
                        bat 'mvn test'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Tests failed: ${e.message}"
                    }
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                // Using SonarQube for code analysis
                script {
                    try {
                        bat 'mvn sonar:sonar'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Code analysis failed: ${e.message}"
                    }
                }
            }
        }

        stage('Security Scan') {
            steps {
                // Using OWASP Dependency-Check for security scanning
                script {
                    try {
                        bat 'mvn dependency-check:check'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Security scan failed: ${e.message}"
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Deploying to AWS EC2 instance
                script {
                    try {
                        bat 'scp target\\myapp.jar ec2-user@staging-server:/path/to/deploy'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Deploy to Staging failed: ${e.message}"
                    }
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Running integration tests on staging
                script {
                    try {
                        bat 'ssh ec2-user@staging-server "/path/to/run-tests.sh"'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Staging integration tests failed: ${e.message}"
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                // Deploying to production server
                script {
                    try {
                        bat 'scp target\\myapp.jar ec2-user@production-server:/path/to/deploy'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                        error "Deploy to Production failed: ${e.message}"
                    }
                }
            }
        }
    }

    post {
        success {
            script {
                emailext (
                    subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Good news! The build ${env.JOB_NAME} #${env.BUILD_NUMBER} completed successfully.",
                    to: "${env.EMAIL_RECIPIENT}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
        failure {
            script {
                emailext (
                    subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Unfortunately, the build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed. Please check the logs for details.",
                    to: "${env.EMAIL_RECIPIENT}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
    }
}
