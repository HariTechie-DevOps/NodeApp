pipeline {
    agent { label 'docker-agent' }

    stages {

        stage('Cleanup Old Container') {
            steps {
                sh 'docker rm -f nodeapp || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodeapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3001:3000 --name nodeapp nodeapp'
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
