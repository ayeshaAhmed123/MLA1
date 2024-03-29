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
            }
        }
    }
    post {
        success {
            // Notifying the administrator via email on success
            emailext body: "Your Docker image ${registry}/${image_name}:${image_tag} has been successfully pushed to DockerHub.",
                     subject: 'Docker Image Pushed Successfully',
                     to: 'i202424@nu.edu.pk'
        }
        failure {
            // Notifying the administrator via email on failure
            emailext body: "There was a problem building or pushing the Docker image ${registry}/${image_name}:${image_tag}.",
                     subject: 'Docker Image Build Failed',
                     to: 'i202424@nu.edu.pk'
        }
    }
}
