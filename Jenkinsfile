pipeline {
  environment {
    dockerimagename = "sasodimovski/react-app"
    dockerImage = ""
	KUBECONFIG = "${HOME}/.kube/config"
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        git 'https://github.com/SasoDimovski/jenkins-kubernetes-deployment.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
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
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
		 sh 'kubectl config use-context minikube'
		 sh ‘kubectl apply -f deployment.yaml’
		 sh ‘kubectl apply -f service.yaml’
        }
      }
    }
  }
}