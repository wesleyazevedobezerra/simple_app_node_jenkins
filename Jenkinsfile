pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simple-app-node-jenkins .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker tag simple-app-node-jenkins wesleyab/simple-app-node-jenkins'
                sh 'docker push wesleyab/simple-app-node-jenkins'
            }
        }
    }

    post {
        always {
            // Executa logout em node com docker instalado
            node {
                sh 'docker logout || true'
            }
        }
    }
}
