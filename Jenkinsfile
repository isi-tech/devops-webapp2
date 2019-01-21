pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2/', branch: 'master')
      }
    }
    stage('Compile') {
      agent {
        node {
          label 'agent1'
        }

      }
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
    stage('Docker') {
      agent {
        node {
          label 'agent1'
        }

      }
      steps {
        sh '''cp ./build/libs/*.war ./docker
cd ./docker
pwd
ls -la
'''
        unstash 'WAR'
        sh '''cd ./docker
pwd
ls -la
docker build -t webapp1:latest .
docker images'''
      }
    }
  }
}