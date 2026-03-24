pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HariTechie-DevOps/NodeApp.git'
            }
        }

        stage('Stop Old Container') {
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
                sh 'docker run -d -p 3000:3000 --name nodeapp nodeapp'
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
