pipeline {
  agent {
    docker {
      image 'node:14-alpine'
      args '--user root' // Run container as root
    }
  }
  stages {
    stage('Install dependencies') {
      steps {
        sh 'apk update && apk add --no-cache --virtual .build-deps gcc g++ make python3' // Install build dependencies
        sh 'apt-get update && apt-get install -y npm' // Install npm using apt-get
      }
    }
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install') {
      steps {
        sh 'npm ci'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Deploy') {
      steps {
        sh 'pm2 start ecosystem.config.js'
      }
    }
  }
}
