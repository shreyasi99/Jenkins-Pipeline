pipeline {
    agent any
    environment {
        AWS_ACCOUNT_ID="955848117495"
        AWS_DEFAULT_REGION="us-east-2" 
        IMAGE_REPO_NAME="mydockerrepo"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "955848117495.dkr.ecr.us-east-2.amazonaws.com/mydockerrepo"
    }
    stages{
     stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/shreyasi99/Jenkins-Pipeline.git']]])
            }
     }
   

  
    // Building Docker images
    
        stage('build') {
            steps {
                echo "Demo on github Webhooks!"
        }
      }
       stage('Logging into AWS ECR') {
            steps {
                script {
                  sh "aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"
                }
                 
            }
        }
        stage('Pushing to ECR') {
     steps{  
         script {
                sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${REPOSITORY_URI}:$IMAGE_TAG"
                sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"
         }
        }
      }
     
    }


}

