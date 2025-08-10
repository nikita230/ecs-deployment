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
              sh "docker build -t python-app ."
           }
        }

        stage('Push to ECR'){
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws creds'  
                ]])
                {
                sh " aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 921500610579.dkr.ecr.eu-north-1.amazonaws.com/python-app"
                sh "docker tag python-app 921500610579.dkr.ecr.eu-north-1.amazonaws.com/python-app:${env.BUILD_NUMBER}"
                sh " docker push 921500610579.dkr.ecr.eu-north-1.amazonaws.com/python-app:${env.BUILD_NUMBER}"
                }
                }
        }

      
    }
}

        
