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
            when {
                changeset "**/api/**/*.*"
            }
            steps {
                dir('api') {
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID .'
                    sh 'docker run -p 8800:8800 --env-file .env $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                }
                sh 'Build Client Done'

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
                
                sh 'Build Client Done'

            }
        }

        stage('logout') {
            steps {
                sh 'docker logout'
            }
        }
    }
}
