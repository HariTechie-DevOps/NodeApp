pipeline {
    agent none

    stages {

        stage('Build & Deploy') {
            parallel {

                stage('DEV') {
                    when {
                        branch 'dev'
                    }
                    agent any

                    stages {
                        stage('Build Image') {
                            steps {
                                sh 'docker build -t nodeapp:dev .'
                            }
                        }

                        stage('Run Container') {
                            steps {
                                sh '''
                                docker rm -f nodeapp-dev || true
                                docker run -d -p 3001:3000 --name nodeapp-dev nodeapp:dev
                                '''
                            }
                        }
                    }
                }
            }
        }
    }
}
