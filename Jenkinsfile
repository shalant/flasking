pipeline {
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
    stage('Docker Login') {
      steps {
        sh 'docker login -u dougrosenbergdev -p a1c8b9c4-ef65-4030-8e69-d90f13ab9795'
      }
    }
    stage('Build') {
      steps {
        echo 'building'
        sh 'docker build -t dougrosenbergdev/flask_app .'
      }
    }
    stage('Docker Push') {
      steps {
        sh 'docker push dougrosenbergdev/flask_app'
      }
    }
     stage('Clean Up') {
      steps {
        echo 'cleaning'
        sh 'docker image prune -af'
      }
    }

  }
}