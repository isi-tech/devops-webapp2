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
        sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build
'''
      }
    }
  }
}