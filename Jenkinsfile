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

        stage('k8s deployment') {
             steps {
                script {
                sh "aws eks update-kubeconfig --region us-east-1 --name ascode-cluster"
                sh "sleep 5"
                sh "kubectl apply -f deployment.yaml"
                sh "kubectl get services"
                echo 'File is deployed inside our Cluster!'
                
                // in this case Jenkins doesn't need withCredentials() to AWS, because the creadential are already saved as GLOBAL inside Jenkins Credentials
                }
            }
        } 
    }
}

// to run JenkinsServer Image using Docker: docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock dantej/jenkins-docker-kubectl-awscli
// AND IMPORTANT: luego para resolver el problema del root "CANNOT CONNECT TO THE DOCKER DAEMON AT UNIX:/VAR/RUN/DOCKER.SOCK":  chown 1000:1000 /var/run/docker.sock

// para lo anterior, se debe entrar dentro del Jenkins Server he instalar docker como SUPER USUARIO/ROOT:     docker exec -u 0 -it (CONTAINER-ID) bash 
