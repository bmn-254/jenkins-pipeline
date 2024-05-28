pipeline {
    agent any
    stages {
        stage('Check Connectivity') {
            steps {
                sh 'ping -c 4 smtp.gmail.com'
                sh 'nc -zv smtp.gmail.com 465'  // Adjust port as needed
            }
        }
    }
}
