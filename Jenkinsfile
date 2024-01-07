pipeline {
    agent none
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dh_cred')
    }
    stages {
        stage('Checkout'){
            agent any
            steps{
                checkout scm
            }
        }

        stage('Init'){
            agent any
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Build API'){
            agent any
            when {
              changeset "**/api/**/*.*"
                beforeAgent true
           }
            steps {
                dir('api'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/api:$BUILD_ID'
                }
            }
        }

        stage('Build Client'){
            agent any
            when {
               changeset "**/client/**/*.*"
               beforeAgent true
              }
            steps {
                dir('client'){
                    sh 'docker build -t $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID .'
                    sh 'docker push $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                    sh 'docker rmi $DOCKERHUB_CREDENTIALS_USR/client:$BUILD_ID'
                }
            }
        }
        stage('logout'){
            agent any
            steps {
                sh 'docker logout'
            }
        }

    }
}