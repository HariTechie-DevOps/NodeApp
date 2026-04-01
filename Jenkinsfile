pipeline {
    agent none

    stages {

        stage('Build & Deploy') {
            parallel {

                stage('DEV') {
                    when {
                        branch 'dev'
                    }
                    agent { label 'dev' }

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

                stage('FEATURE') {
                    when {
                        branch 'feature/test'
                    }
                    agent { label 'feat' }

                    stages {
                        stage('Build Image') {
                            steps {
                                sh 'docker build -t nodeapp:feat .'
                            }
                        }

                        stage('Run Container') {
                            steps {
                                sh '''
                                docker rm -f nodeapp-feat || true
                                docker run -d -p 3002:3000 --name nodeapp-feat nodeapp:feat
                                '''
                            }
                        }
                    }
                }

                stage('MAIN') {
                    when {
                        branch 'main'
                    }
                    agent label { 'dev' }

                    stages {
                        stage('Build Image') {
                            steps {
                                sh 'docker build -t nodeapp:main .'
                            }
                        }

                        stage('Run Container') {
                            steps {
                                sh '''
                                docker rm -f nodeapp-main || true
                                docker run -d -p 3000:3000 --name nodeapp-main nodeapp:main
                                '''
                            }
                        }
                    }
                }
            }
        }
    }
}
