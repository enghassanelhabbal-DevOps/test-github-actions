pipeline {
  agent { label 'node-agent' }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/AbdelrhmanEzzat/digi-jenkins.git'
      }
    }

    stage('Install') {
      steps {
        sh '''
          export NVM_DIR="$HOME/.nvm"
          [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
          npm install
        '''
      }
    }

    stage('Test') {
      steps {
        sh '''
          export NVM_DIR="$HOME/.nvm"
          [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
          npm test
        '''
      }
    }
  }

  post {
    success { echo '✅ All tests passed on EC2!' }
    failure  { echo '❌ Build failed!' }
    always   { cleanWs() }
  }
}
