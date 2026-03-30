pipeline {
    agent { label 'docker-agent' }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/HariTechie-DevOps/NodeApp.git'
            }
        }

        stage('Cleanup Old Container') {
            steps {
                sh 'docker rm -f nodeapp || true'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t nodeapp .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name nodeapp nodeapp'
            }
        }
    }
}
