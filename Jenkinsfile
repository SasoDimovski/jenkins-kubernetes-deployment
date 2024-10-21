pipeline {
  environment {
    dockerimagename = "sasodimovski/react-app"
    dockerImage = ""
	KUBECONFIG = "C:\\Users\\SASHO\\.kube\\config"
  }
  agent any
  stages {
    stage('Pull од GitHub') {
      steps {
        git 'https://github.com/SasoDimovski/jenkins-kubernetes-deployment.git'
      }
    }
    stage('Build на Docker image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Push на DockerHub') {
      environment {
          registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploy на Kubernetes ') {
      steps {
          script {
		 bat 'kubectl apply -f deployment.yaml'
		 bat 'kubectl apply -f service.yaml'
        }
      }
    }
  }
}

