pipeline {
  agent {
    docker {
      image 'gradle:4.10.2-jdk8'
    }

  }
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2.git', branch: 'master')
      }
    }
    stage('Info') {
      steps {
        sh '''echo BUILD_ID = $BUILD_ID
echo JENKINS_URL = $JENKINS_URL
echo PATH = $PATH'''
      }
    }
  }
}