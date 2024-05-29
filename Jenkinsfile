pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'nkongebryan44@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    writeFile file: 'build.log', text: 'Build log content here...'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    writeFile file: 'test.log', text: 'Test log content here...'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    writeFile file: 'code_analysis.log', text: 'Code analysis log content here...'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    writeFile file: 'security_scan.log', text: 'Security scan log content here...'
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Sending email notification...'
                emailext (
                    subject: "Build ${currentBuild.result}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: """<p>Build ${currentBuild.result}: ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
                             <p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME} #${env.BUILD_NUMBER}</a> to view the results.</p>""",
                    to: "${env.EMAIL_RECIPIENT}",
                    attachmentsPattern: '**/*.log'
                )
            }
        }
    }
}
