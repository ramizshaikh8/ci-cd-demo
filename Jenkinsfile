pipeline {
  agent any
  tools {
      go 'gotest'
  }
  environment {
      GO111MODULE='on'
  }
  
  stages {
    stage('Test') {
      steps {
        git 'https://https://github.com/ramizshaikh8/ci-cd-demo4.git'
        sh 'go test ./...'
      }
    }
    stage('Build') {
        steps {
        git 'https://https://github.com/ramizshaikh8/ci-cd-demo4.git'
        sh 'go build .'
        }
    }
    stage('Run') {
        steps {
            sh 'cd /var/lib/jenkins/workspace/full-cicd-go && go-webapp-sample &'
        }
    }

  }
}
