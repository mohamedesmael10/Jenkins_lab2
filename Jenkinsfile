pipeline {
    agent any
    environment {
        DOCKER_CREDS = credentials('mohamedesmael_dockerhub')
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mohamedesmael10/Jenkins_lab2.git', branch: 'test'
            }
        }
        stage('Docker Login') {
            steps {

                sh '''
                  echo "\$DOCKER_CREDS_PSW" | docker login -u "\$DOCKER_CREDS_USR" --password-stdin
                '''
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t ubuntu .'
            }
        }
        stage('Tag Image') {
            steps {
                sh 'docker tag ubuntu mohamedesmael/jenkins_lab1:v3'
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push mohamedesmael/jenkins_lab1:v3'
            }
        }
    }
}
