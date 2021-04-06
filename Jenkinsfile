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
                withDockerRegistry(credentialsId: 'jenkins-credentials', url: 'https://index.docker.io/v1/')  
                   { 
                    sh "docker build -t jenkins-demo:${BUILD_NUMBER} ." 
                    sh "docker tag jenkins-demo:${BUILD_NUMBER} jenkins-demo:latest"
                    sh "docker push $registry:$BUILD_NUMBER"   
                    }
            } 
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
    post {
        always {
            emailext body: 'Test mail alert', subject: 'Alert Email', to: 'leanhtu.0404@gmail.com'
        }
    }
}
