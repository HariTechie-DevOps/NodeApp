pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'docker build -t nodeapp:${BRANCH_NAME} .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f nodeapp || true
                docker run -d -p 3000:3000 --name nodeapp nodeapp:${BRANCH_NAME}
                '''
            }
        }
    }
}
