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
        sh 'docker login -u dougrosenbergdev -p Blahblah1!'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker build -t flask_app:latest'
      }
    }

  }
}