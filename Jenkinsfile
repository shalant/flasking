pipeline {

  environment {
    registry = 'dougrosenbergdev/flask_app'
    registryCredentials = 'docker'
    cluster_name = 'skillstorm'
    namespace = 'drosenberg'
  }

  agent {
    node {
      label 'docker'
    }
  }

  stages {
    stage('git') {
      steps {
        git(url: 'https://github.com/shalant/flasking.git', branch: 'master')
      }
    }
    stage('Build Stage') {
      steps {
        script {
          dockerImage = docker.build(registry)
        }
      }
    }
    stage('Deploy Stage') {
      steps {
        script {
          docker.withRegistry('', registryCredentials) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Kubernetes') {
      steps {
        withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsID: 'AWS', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh "aws eks update-kubeconfig --region us-east-1 --name ${cluster_name}"
          sh "kubectl create namespace drosenberg ${namespace}"
          sh "kubectl apply -f deployment.yaml -n ${namespace}"
          sh "kubectl -n ${namespace} rollout restart deployment flaskcontainer"
        }
      }
    }
  }
}