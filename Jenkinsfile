pipeline {
    agent any 
    environment {
        AWS_ACCOUNT_ID = '322742385274'
        AWS_DEFAULT_REGION = 'ap-south-1'
        IMAGE_REPO_NAME = 'frontend'
        IMAGE_TAG = 'latest'
        REPOSITORY_URI = '322742385274.dkr.ecr.ap-south-1.amazonaws.com/frontend'
    }
    stages {
        stage('Logging into AWS ECR') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 322742385274.dkr.ecr.ap-south-1.amazonaws.com'
                }
            }
        }
        stage('Cloning Git') { 
            steps { 
                checkout scm
            }
        } 
        stage('Building image') { 
            steps { 
                script { 
                    dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
                }
            } 
        }
        stage('Pushing to ECR') {
            steps {
                script {
                    sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:$IMAGE_TAG"
                    sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"
                }
            }
        }     
    }
}