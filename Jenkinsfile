pipeline {
    agent any 
    stages {
        stage('Cloning Git') { 
            steps { 
                checkout scm
            }
        } 
        stage('Building image') { 
            steps { 
                script { 
                    dockerImage = docker.build('himanshi321/getting-started:latest') 
                }
            } 
        }     
    }
}