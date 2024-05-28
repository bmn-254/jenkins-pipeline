pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool - Maven to compile and package the code."
            }
            post {
                success {
                    script {
                        try {
                            emailext(
                                to: "nkongebryan44@gmail.com",
                                subject: "Build Status",
                                body: "The build status was a success!"
                            )
                        } catch (Exception e) {
                            echo "Error sending email: ${e.getMessage()}"
                            e.printStackTrace()
                        }
                    }
                }
                failure {
                    script {
                        try {
                            emailext(
                                to: "nkongebryan44@gmail.com",
                                subject: "Build Failed",
                                body: "The build failed."
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
