pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Project Building Begins...'
        powershell 'mvn clean package'
      }
    }

    stage('Unit and Integration Tests') {
      steps {
        echo 'Running unit and integration tests...'
        powershell 'mvn test'
      }
      post {
        always {
          emailext(
            to: 'nkongebryan44@gmail.com',
            subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} Test Results",
            body: "The Test stage of the Build ${env.JOB_NAME} #${env.BUILD_NUMBER} has finished with status: ${currentBuild.currentResult}",
            attachLog: true
          )
        }
      }
    }

    stage('Code Analysis') {
      steps {
        echo 'Performing static code analysis...'
        powershell 'sonar-scanner'
      }
    }

    stage('Security Scan') {
      steps {
        echo 'Scanning for security vulnerabilities...'
        powershell 'dependency-check --project MyProject'
      }
      post {
        always {
          emailext(
            to: 'nkongebryan44@gmail.com',
            subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} Security Scan Results",
            body: "The Security Scan stage of Build ${env.JOB_NAME} #${env.BUILD_NUMBER} has finished with status: ${currentBuild.currentResult}",
            attachLog: true
          )
        }
      }
    }

    stage('Deploy to Staging') {
      steps {
        echo 'Deploying to the staging environment...'
        powershell 'aws deploy --stage staging'
      }
    }

    stage('Integration Tests on Staging') {
      steps {
        echo 'Running integration tests on the staging environment...'
        powershell 'newman run staging-collection.json'
      }
    }

    stage('Deploy to Production') {
      steps {
        echo 'Deploying to the production environment...'
        powershell 'aws deploy --stage production'
      }
    }
  }

  post {
    always {
      echo 'Pipeline execution completed'
    }
    failure {
      echo 'Pipeline failed'
    }
  }
}
