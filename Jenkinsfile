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

                        sh "aws eks update-kubeconfig --region us-east-1 --name ascode-cluster"
                        sh "kubectl get services"
                        // sh "kubectl apply -f  deployment.yaml"
                }
            }
        } 

        // stage('k8s deployment') {
        //      steps {
        //         script {
        //         withKubeConfig([credentialsId: 'K8S', serverUrl: '']) {
        //         sh ('kubectl apply -f  deployment.yaml')
        //             }
        //         }
        //     }
        // } 

        stage('Input to remove POD from AWS EKS') {
             steps {
                echo 'Adding INPUT to remove POD in EKS'
            }
        }  

    }
}

// to run JenkinsServer Image using Docker: docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock dantej/jenkins-docker-kubectl-awscli
// AND IMPORTANT: luego para resolver el problema del root "CANNOT CONNECT TO THE DOCKER DAEMON AT UNIX:/VAR/RUN/DOCKER.SOCK":  chown 1000:1000 /var/run/docker.sock

// para lo anterior, se debe entrar dentro del Jenkins Server he instalar docker como SUPER USUARIO/ROOT:     docker exec -u 0 -it (CONTAINER-ID) bash 
