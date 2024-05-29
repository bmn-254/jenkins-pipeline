pipeline {
    agent any

    environment {
        // Define environment variables for email configuration
        EMAIL_RECIPIENT = 'nkongebryan44@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Simulate build log
                    writeFile file: 'build.log', text: 'Build log content here...'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Simulate test log
                    writeFile file: 'test.log', text: 'Test log content here...'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    // Simulate code analysis log
                    writeFile file: 'code_analysis.log', text: 'Code analysis log content here...'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Simulate security scan log
                    writeFile file: 'security_scan.log', text: 'Security scan log content here...'
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'Sending success email notification...'
                emailext (
                    subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "The build completed successfully. Logs are attached.",
                    to: "${env.EMAIL_RECIPIENT}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
        failure {
            script {
                echo 'Sending failure email notification...'
                emailext (
                    subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "The build failed. Please check the attached logs for details.",
                    to: "${env.EMAIL_RECIPIENT}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
    }
}
