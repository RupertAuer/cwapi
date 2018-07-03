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
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -f ./cwapi/Dockerfile .'
      }
    }
    stage('') {
      steps {
        script {
          app = docker.build('mywoshtestregistry.azurecr.io/cwapi')
          docker.withRegistry('https://mywoshtestregistry.azurecr.io', 'acr-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push('latest')
          }
        }

      }
    }
  }
}