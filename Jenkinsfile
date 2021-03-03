pipeline {
    environment {
    registry = "niraj1286/docker_nodejs"
    registryCredential = "dockerhub"
    dockerImage = ''
    PATH = "$PATH:/usr/local/bin"
}

    agent any
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/niraj1201/Docker_Jenkins_Pipeline'
                }
            }

            stage('Building Docker Image') {
                steps {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }

            stage('Deploying Docker Image to Dockerhub') {
                steps {
                    script {
                        docker.withRegistry('', registryCredential) {
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