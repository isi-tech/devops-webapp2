pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2/', branch: 'master')
      }
    }
    stage('Compile') {
      steps {
        tool(name: 'gradle-4.10.2', type: 'gradle')
        sh 'sh "gradle build"'
      }
    }
  }
}