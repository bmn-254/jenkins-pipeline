pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Use a build automation tool such as Maven or Gradle to compile and package the code."
            }
           
            post {
                success {
                    mail to: "nkongebryan44@gmail.com",
                    subject: "Build status",
                    body: "The build was successful!"
                }
            }
        } // Close stage('Build')

        stage('Unit and Integration Tests') {
            steps {
                echo " Use test automation tools like JUnit or TestNG for unit tests and integration tests."
            }
        } // Close stage('Unit and Integration Tests')

        stage('Code Analysis') {
            steps {
                echo " Integrate a code analysis tool like SonarQube or Checkstyle for code quality checks."
            }
        } // Close stage('Code Analysis')

        stage('Security Scan') {
            steps {
                echo " Perform a security scan using a tool like OWASP ZAP or SonarQube Security Scanner."
            }
        } // Close stage('Security Scan')

        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging server using deployment tools like Ansible or Docker."
            }
        } // Close stage('Deploy to Staging')

        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment to ensure the application works correctly."
            }
        } // Close stage('Integration Tests on Staging')

        stage('Deploy to Production') {
            steps {
                echo " Deploy the application to a production server using deployment tools like Ansible or Docker."
            }
        } // Close stage('Deploy to Production')

    } // Close stages
} // Close pipeline
