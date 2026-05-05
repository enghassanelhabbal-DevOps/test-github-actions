# digi-jenkins


pipeline {
  agent { label 'ec2' }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/AbdelrhmanEzzat/digi-jenkins.git'
      }
    }

    stage('Install') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh 'npm test'
      }
    }

  }

  post {
    success { echo '✅ All tests passed on EC2!' }
    failure  { echo '❌ Build failed!' }
    always   { cleanWs() }
  }
}
