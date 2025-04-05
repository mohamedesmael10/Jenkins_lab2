pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mohamedesmael10/Jenkins_lab2.git'
            }
        }
        stage('Docker Login') {
            steps {

                sh '''
                  echo "$PASS" | docker login -u "$USER" --password-stdin
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
                sh 'docker tag ubuntu mohamedesmael/jenkins_lab1:v2'
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push mohamedesmael/jenkins_lab1:v2'
            }
        }
    }
}
