pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Init') {
            steps {
                sh 'echo Init Step'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Build API') {
            
            steps {
                dir('api') {
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                }
                sh 'Build Client Done'

            }
        }

        stage('Build Client') {
            
            steps {
                dir('client') {
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                }
            }
        }

        stage('logout') {
            steps {
                sh 'docker logout'
            }
        }
    }
}
