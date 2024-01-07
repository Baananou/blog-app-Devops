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
                sh 'echo $DOCKERHUB_CREDENTIALS_USR'
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Build API') {
            when {
                changeset "**/api/**/*.*"
            }
            steps {
                dir('api') {
                    sh 'echo $DOCKERHUB_CREDENTIALS_USR'
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID .'
                    sh 'docker run -p 8800:8800 --env-file .env $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                }
            }
        }

        stage('Build Client') {
            when {
                changeset "**/client/**/*.*"
            }
            steps {
                dir('client') {
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID .'
                    sh 'docker run -p 3000:3000 --env-file $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
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
