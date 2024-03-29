pipeline {
    environment {
        registry = "ayeshaahmed123/mlops_assignment1"
        registryCredential = 'git'
        dockerImage = ''
        image_name = 'FlaskApp_hamza_ayesha'
        image_tag = 'latest' 
    }
    agent any
    stages {
        stage('Cloning Git Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ayeshaAhmed123/MLA1.git'
            }
        }
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}/${image_name}:${image_tag}")
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
                emailext body: 'Your Docker image has been successfully pushed to DockerHub.',
                             subject: 'Docker Image Pushed Successfully',
                             to: 'ahmedayesha2402@gmail.com'
            }
        }
    }
}
