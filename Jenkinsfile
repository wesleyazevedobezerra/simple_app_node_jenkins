pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }

    stages {
        stage('Clone Git Repository') {
            steps {
                 git branch: 'main', url: 'https://github.com/wesleyazevedobezerra/simple_app_node_jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t wesleyab/simple-app-node-jenkins .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push wesleyab/simple-app-node-jenkins'
            }
        }
    }

    post {
        always {
            echo 'Logging out from Docker...'
            sh 'docker logout'
        }
    }
}
