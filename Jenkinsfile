pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/oumaimajallouli/Oumaima-Jallouli-front.git', branch: 'main'
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'npm install --legacy-peer-deps'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
  }
}
