pipeline {
  agent any
  environment {
    NODE_PATH = 'C:/Program Files/nodejs'
    SONAR_SCANNER_PATH = 'C:/Program Files/sonar-scanner-6.2.1.4610-windows-x64/bin'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        script {
          bat 'npm install'
        }
      }
    }

    stage('Sonarcube Analysis') {
      environment {
        SONAR_TOKEN = credentials('sonar-token')
      }
      steps {
        script {
                bat '''
                    set PATH=%NODE_PATH%;%SONAR_SCANNER_PATH%;%PATH%
                    "%SONAR_SCANNER_PATH%/sonar-scanner.bat" -Dsonar.projectKey=register-backend ^
                    -Dsonar.sources=. ^
                    -Dsonar.host.url=http://localhost:9000 ^
                    -Dsonar.login=%SONAR_TOKEN%
                '''
            }
      }
    }
  }

  post {
    success {
      echo "Pipeline success"
    }
    failure {
      echo "Pipeline failed"
    }
  }
}
