pipeline {
    environment {
        registry = "leanhtu0404/docker-jenkins"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent { label 'jenkins-slave' }
    stages {
        stage ('Clone') {
            steps {
                git 'https://github.com/leanhtu0404/jenkins-github'
            }
        }
        stage('Building image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                    dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}
