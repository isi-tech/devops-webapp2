pipeline {
  agent any
  stages {
    stage('Checkout') {
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
./gradlew build'''
        stash(name: 'WAR', includes: 'build/libs/*.war')
      }
    }
    stage('Deploy') {
      steps {
        unstash 'WAR'
      }
    }
    stage('Docker') {
      agent {
        node {
          label 'agent1'
        }

      }
      steps {
        sh 'docker ps'
      }
    }
  }
}