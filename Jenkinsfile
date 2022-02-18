pipeline {
    agent {label "docker_build"}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_bango')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/Anil-55/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t anildevops45/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push anildevops45/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
