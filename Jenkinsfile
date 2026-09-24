pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/youssef060902/Timesheet-DevOps.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
    }
}
