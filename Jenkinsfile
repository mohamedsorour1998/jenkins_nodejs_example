pipeline {
  agent { node { label 'jenkins_slave' } }
  stages {
    stage('Install dependencies') {
      steps {
        sh 'apk add --no-cache npm' // Install npm using Alpine package manager
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
