
pipeline {
    agent { label 'ubuntu' }

    stages {
        stage('Check Tools') {
            steps {
                sh 'git --version'
                sh 'docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t codealpha-jenkins-remoting .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f codealpha-test || true
                    docker run -d \
                        --name codealpha-test \
                        -p 5001:5000 \
                        codealpha-jenkins-remoting
                '''
            }
        }

        stage('Test Application') {
            steps {
                sh '''
                    sleep 5
                    curl --fail http://localhost:5001/health
                '''
            }
        }
    }
}
