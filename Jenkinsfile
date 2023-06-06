pipeline {

  environment {
    registry = "hazza090/flask_app"
    registryCredentials = "docker"
    cluster_name = "skillstorm"
    namespace = "hazza090"
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

    stage('kubernetes') {
      steps {
        withCredentials([aws(accessKeyVariable: 'AWS_CCESS_KEY_ID', credentialsID: 'AWS', secretKeyVariable: "AWS_SECRET_ACCESS_KEY")]) {
            // some block
          sh "aws eks --region us-east-1 update-kubeconfig --name ${cluster_name}"
          script {
            try {
              sh "kubectl create namespace ${namespace}"
            }
            catch (Exception e) {
              echo "Error / namespace already created"
            }
          }
        }
        sh "kubectl appl -f ./deployment.yaml -n ${namespace}"
        sh "kubectl -n ${namespace} rollout restart deployment flaskcontainer"
      }
    }
  }
} 