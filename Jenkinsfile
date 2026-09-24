
pipeline {
    agent { label 'ubuntu' }

    stages {
        stage('Check Ubuntu') {
            steps {
                sh 'uname -a'
            }
        }

        stage('Check Java') {
            steps {
                sh 'java -version'
            }
        }

        stage('Check Git') {
            steps {
                sh 'git --version'
            }
        }

        stage('Check Docker') {
            steps {
                sh 'docker --version'
            }
        }
    }
}
