pipeline {
    agent any
    environment {
        IMAGE='rhoofard/realworld_backend'
        TAG='latest'
    }
    stages {
        stage('Build') {
            steps {
                sh "docker build --pull -t ${IMAGE}:${TAG} ."
            }
        }
        stage('Push to dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerPassword', usernameVariable: 'dockerUsername')]) {
                    sh "docker login -u ${env.dockerUsername} -p ${env.dockerPassword}"
                    sh "docker push ${env.IMAGE}:${TAG}"
                }
            }
        }
    }
}
