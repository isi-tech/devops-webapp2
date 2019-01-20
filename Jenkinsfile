pipeline {
  agent any
  stages {
    stage('Details') {
      steps {
        sh 'echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"'
      }
    }
  }
}