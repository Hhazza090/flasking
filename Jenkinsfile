pipeline {

  environment {
    registry = "hazza090/flask_app"
    registryCredentials = "docker"
    cluster_name = "skillstorms"
  }
  
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

    stage ('Build Stage') {
       steps {
        script {
            dockerImage = docker.build(registry)
        }
       }
    }  

    stage('Deployment Stage') {
      steps{
        script {
            docker.withRegistry('', registryCredentials) {
                dockerImage.push()
            }

        }
      }
    }
  }
} 