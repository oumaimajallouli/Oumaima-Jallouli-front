pipeline {
  agent any

  environment {
    SONARQUBE_SERVER = 'sonarqube'  // Le nom de ta configuration SonarQube dans Jenkins
  }

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

    stage('SonarQube analysis') {
    steps {
      withSonarQubeEnv(SONARQUBE_SERVER) {
        sh '''
          npx sonar-scanner \
            -Dsonar.projectKey=OumaimaFront \
            -Dsonar.sources=src \
            -Dsonar.host.url=$SONAR_HOST_URL \
            -Dsonar.login=$SONAR_AUTH_TOKEN
        '''
        }
      }
    }

    
  }
}
