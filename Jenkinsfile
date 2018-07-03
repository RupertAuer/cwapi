pipeline {
  agent any
  stages {
    stage('DotNet Build') {
      agent {
        docker {
          image 'microsoft/dotnet'
        }

      }
      steps {
        sh 'dotnet build cwapi.sln'
      }
    }
    stage('Docker Build and Push') {
      steps {
        script {
          sh "docker build -t mywoshtestregistry.azurecr.io/cwapi  -f ./cwapi/Dockerfile ."
        }

        script {
          withCredentials([usernamePassword(credentialsId: 'acr-credentials', passwordVariable: 'acrPassword', usernameVariable: 'acrUser')]) {
            sh "docker login -u ${env.acrUser} -p ${env.acrPassword}"
            sh 'docker push mywoshtestregistry.azurecr.io/cwapi'

          }
        }

      }
    }
  }
}