pipeline {
    agent any
    tools {
    maven 'MAVEN'
        }
    /*environment {
        registry = "664201875222.dkr.ecr.us-east-2.amazonaws.com/imagerepo"
    }*/    
    stages {
        stage('GitCheckout') {
            steps {
                git branch: 'main', credentialsId: 'GITHUB_CREDS', url: 'https://github.com/jayashri27/NSpringBoot'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('TruffleHog'){
            steps{
              sh 'docker run -t trufflesecurity/trufflehog:latest github --no-update --repo  https://github.com/jayashri27/NSpringBoot.git > report'
              sh  'cat report' 
            }
        }
        /*stage('docker login'){
            steps{
            withCredentials([string(credentialsId: 'Docker_Hub', variable: 'PASSWORD')]) {
            sh 'docker login -u jayashrimahale22 -p $PASSWORD'
            }
          }
        }*/
        /*stage('Building image') {
           steps{
            script {
          dockerImage = docker.build registry 
                 }
              }
          }
        stage('Pushing to ECR') {
           steps{  
           script {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 664201875222.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker push 664201875222.dkr.ecr.us-east-1.amazonaws.com/imagerepo:latest'
         }
        }
      }
        stage('kubernetes_deployment'){
            steps{
                sh 'kubectl apply -f eks-deploy-k8s.yaml'
            }
        }*/
    }
}
