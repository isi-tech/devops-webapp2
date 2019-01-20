pipeline {
  agent any
  stages {
    stage('Test') {
      steps {
        tool(name: 'gradle-4.10.2', type: 'gradle')
      }
    }
  }
}