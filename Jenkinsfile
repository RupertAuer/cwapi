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
          docker.withRegistry('https://mywoshtestregistry.azurecr.io', 'acr-credentials') {
            def img = docker.image(mywoshtestregistry.azurecr.io/cwapi)
            img.push('latest')

          }
        }

      }
    }
  }
}