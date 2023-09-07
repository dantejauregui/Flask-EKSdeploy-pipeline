pipeline {
    environment {
    registry = "dantej/flask-ec2deploy"
    registryCredential = 'dockerhubaccount'
    dockerImage = ''
  }

    agent any

    stages {
        stage('Test the Jenkinsfile') {
            steps {
                 echo 'Test the Jenkinsfile'
                 echo 'Test the Jenkinsfile successfully'
            }
        }

        stage('Accessing EKS and deploying new Kubernetes App') {
             steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-jenkins-ec2deploy',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {

                        sh "aws ec2 describe-instances --region=eu-central-1"
                }
            }
        } 

        stage('Input to remove POD from AWS EKS') {
             steps {
                echo 'Adding INPUT to remove POD in EKS'
            }
        }  

        
    }
}

