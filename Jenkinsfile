pipeline {
  agent any
  environment {
    WEBROOT = '/var/www/portfolio'
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        echo 'Static site - no build step required'
      }
    }
    stage('Deploy') {
      steps {
        sh '''
          mkdir -p ${WEBROOT}
          rsync -r --delete --exclude='.git' "${WORKSPACE}/" "${WEBROOT}/"
        '''
      }
    }
  }
  post {
    success {
      echo "Deployed to ${WEBROOT}"
    }
    failure {
      echo "Pipeline failed - check console output"
    }
  }
}
