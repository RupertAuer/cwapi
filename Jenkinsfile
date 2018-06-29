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
        sh 'docker build -t cwapi/Dockerfile'
      }
    }
  }
}