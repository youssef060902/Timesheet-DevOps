pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/OnsBENSALAH/Timesheet-DevOps.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
    }
}
