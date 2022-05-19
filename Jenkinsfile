pipeline {
  agent any
  stages {
    stage('git') {
      steps {
        git(url: 'https://github.com/shalant/flasking.git', branch: 'master')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t flask_app .'
      }
    }

    stage('Docker Login') {
      steps {
        sh 'docker login -u dougrosenbergdev -p a1c8b9c4-ef65-4030-8e69-d90f13ab9795'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker build -t flask_app:latest'
      }
    }

  }
}