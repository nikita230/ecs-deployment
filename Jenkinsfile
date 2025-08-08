pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                git credentialsId: 'c8d9ecb0-d5fb-4f2f-8259-52cac87a2a3e',  
                    url: 'https://github.com/nikita230/ecs-deployment.git',
                    branch: 'main'
            }
        }

        stage('Build') {
           steps {
              sh "docker build -t python-app:${env.BUILD_NUMBER} ."
           }
        }

        stage('Push to ECR'){
            steps {
                sh " aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 921500610579.dkr.ecr.eu-north-1.amazonaws.com/python"
            }
        }




        
    }
}

        
