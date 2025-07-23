pipeline {
    agent any

    environment {
      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }


    stages {
        stage('gitclone') {
            steps {
               git 'https://github.com/wesleyazevedobezerra/simple_app_node_jenkins.git'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t simple-app-node-jenkins .'
            }
        }

        stage('Login Docker') {
            steps {
                sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
            }
        }

           stage('Push') {
            steps {
                sh 'docker push wesleyab/simple-app-node-jenkins'
            }
        }

    }
    post {
        always {
                sh 'docker logout' 
        }
    }
}