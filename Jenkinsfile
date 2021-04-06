pipeline {
    environment {
        registry = "leanhtu0404/docker-jenkins"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage ('Clone') {
            steps {
                git 'https://github.com/leanhtu0404/jenkins-github.git'
            }
        }
        stage ('Build Docker Images') {
            steps {
                script {
                    docker.build registry + ":$BUILD_NUMBER"
                }    
            }    
        }
    }
}
