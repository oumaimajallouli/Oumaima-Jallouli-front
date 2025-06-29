pipeline {
  agent any

  environment {
    SONARQUBE_SERVER = 'SonarQube'  // Le nom de ta configuration SonarQube dans Jenkins
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
              -Dsonar.projectName=OumaimaFront \
              -Dsonar.sources=src \
              -Dsonar.host.url=$SONAR_HOST_URL \
              -Dsonar.login=$SONAR_AUTH_TOKEN \
              -Dsonar.language=js \
              -Dsonar.sourceEncoding=UTF-8
          '''
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 1, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
