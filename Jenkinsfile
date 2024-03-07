// pipeline {
//     agent any
//     stages {
//         stage('Build') { 
//             steps {
//                 sh 'npm install'
//             }
//         }
        
//     }
// }



pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub') // Reference to Docker Hub credentials added in Jenkins credentials
        DOCKER_IMAGE_NAME = 'rudrasanjeev/angular-demo' // Replace with your Docker Hub username and image name
    }
    stages {
        stage('Build') { 
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }
        stage('Docker Build and Push') {
            steps {
                // Authenticate with Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'username', passwordVariable: 'password')]) {
                    sh "sudo docker login -u $username -p $password"
                }
                // Build the Docker image
                 sh "sudo docker build -t $DOCKER_IMAGE_NAME ."
                // Push the Docker image to Docker Hub
                 sh "sudo docker tag angular-demo:latest $DOCKER_IMAGE_NAME"
                 sh "sudo docker push $DOCKER_IMAGE_NAME"
            }
        }
    }
}
