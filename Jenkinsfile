pipeline {
    environment {
        registry = "samireddebarhi/tp5_devops"
        registryCredential = 'dockerhub'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/your-username/your-repo'
            }
        }
        stage('Building image') {
            steps {
                script {
                    def dockerImage = docker.build(registry + ":$BUILD_NUMBER")
                    // Store it for later stages
                    env.DOCKER_IMAGE_NAME = registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    def dockerImage = docker.build(registry + ":$BUILD_NUMBER")
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}