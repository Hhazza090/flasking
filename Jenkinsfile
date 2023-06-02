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

    stage('Docker login') {
      steps {
        sh 'docker login -u hazza090 -p dckr_pat_wJikeqky-eQo9cE-hFP2pbjOGTQ'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t flask_app .'
      }
    }

    stage('Docker Push') {
      steps {
        sh 'docker push hazza090/flask_app .'
      }
    }

  }
}