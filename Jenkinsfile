pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = 'karthikesh03/docker-repo'
    }

    stages {
       stage('Checkout Code') {
    steps {
        git branch: 'main', url: 'https://github.com/Karthikesh2706/docker-repo.git'
    }
}


        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Docker image built and pushed successfully to Docker Hub!'
        }
        failure {
            echo '❌ Build failed. Check console logs for details.'
        }
    }
}
