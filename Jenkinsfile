pipeline {
    environment {
        registry = "leanhtu0404/docker-jenkins"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage ('Clone') {
            steps {
                git 'https://github.com/leanhtu0404/jenkins-github'
            }
        }
        stage ('Build Docker Images') {
            steps {
                sh 'docker build -t tula-1 .'
                }    
            }    
        }
    }
}
