pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2.git', branch: 'master')
      }
    }
    stage('Compile') {
      steps {
        sh 'gradle build'
        tool(name: 'gradle', type: 'gradle-4.10.2')
      }
    }
  }
}