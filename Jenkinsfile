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
          app = docker.build('mywoshtestregistry.azurecr.io/cwapi', '-f ./cwapi/Dockerfile .')
          docker.withRegistry('https://mywoshtestregistry.azurecr.io', 'acr-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push('latest')
          }
        }

      }
    }
  }
}