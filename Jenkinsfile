pipeline {
    environment {
    registry = "278215072102.dkr.ecr.eu-west-1.amazonaws.com/docker_nodejs"
    registryCredential = "ecr:eu-west-1:jenkins-ecs"
    dockerImage = ''
    PATH = "$PATH:/usr/local/bin"
}

    agent any
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/niraj1201/Docker_Jenkins_Pipeline.git'
                }
            }

            stage('Building Docker Image') {
                steps {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                        dockerImage = docker.build registry + ":LATEST"
                    }
                }
            }

            stage('Deploying Docker Image to Dockerhub') {
                steps {
                    script {
                        docker.withRegistry('https://278215072102.dkr.ecr.eu-west-1.amazonaws.com', registryCredential) {
                        dockerImage.push()
                        }
                    }
                }
            }

            stage('Cleaning Up') {
                steps{
                  sh "docker rmi $registry:$BUILD_NUMBER"
                }
            }
        }
    }
