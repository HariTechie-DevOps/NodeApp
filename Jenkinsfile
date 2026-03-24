pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HariTechie-DevOps/NodeApp.git'
            }
        }

        stage('Clean Old Containers') {
            steps {
                sh '''
                docker rm -f nodeapp || true
                docker ps -q --filter "publish=3000" | xargs -r docker rm -f
                '''
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
