pipeline {
    agent any
    triggers {
        pollSCM('*/1 * * * *') // Check every 1 minute
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Récupération du code source"
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Build du projet"
                // Add your build commands here
            }
        }
        stage('Deploy') {
            steps {
                echo "Déploiement du projet"
                // Add your deployment commands here
            }
        }
    }
}