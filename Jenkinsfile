pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      steps {
        git(url: 'https://github.com/Hhazza090/flasking.git', branch: 'main')
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t hazza090/flask_app'
      }
    }

    stage('Docker login') {
      steps {
        sh 'docker login -u hazza090 -p dckr_pat_wJikeqky-eQo9cE-hFP2pbjOGTQ'
      }
    }

    stage('Docker push') {
      steps {
        sh 'docker push hazza090/flask_app'
      }
    }

  }
}