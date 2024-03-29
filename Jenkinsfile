// pipeline {
//     environment {
//         registry = "ayeshaahmed123/mlops_assignment1"
//         registryCredential = 'git'
//         dockerImage = ''
//     }
//     agent any
//     stages {
//         stage('Cloning our Git') {
//             steps {
//                 git 'https://github.com/ayeshaAhmed123/mlopsA1practice.git'
//             }
//         }
//         stage('Building our image') {
//             steps {
//                 script {
//                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
//                 }
//             }
//         }
//         stage('Deploy our image') {
//             steps {
//                 script {
//                     docker.withRegistry('', registryCredential) {
//                         dockerImage.push()
//                     }
//                 }
//             }
//         }
//         stage('Cleaning up') {
//             steps {
//                 sh "docker rmi $registry:$BUILD_NUMBER"
//             }
//         }
//     }
// }
pipeline {
    environment {
        registry = "ayeshaahmed123/mlops_assignment1"
        registryCredential = 'git'
        dockerImage = ''
        recipient_email = 'i202424@nu.edu.pk'
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
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                    // Sending email notification on successful push
                    emailext body: 'Your Docker image has been successfully pushed to DockerHub.',
                             recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                             subject: 'Docker Image Pushed Successfully',
                             to: recipient_email
                }
            }
        }
    }
}
