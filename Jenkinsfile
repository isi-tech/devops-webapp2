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
./gradlew build
ls -la
ls -la build/libs/'''
        stash(name: 'App', includes: 'build/libs/*.war')
      }
    }
    stage('Docker') {
      agent {
        node {
          label 'agent1'
        }

      }
      environment {
        DOCKER_USERNAME = 'aaaaa'
        DOCKER_PASSWORD = 'bbbbbb'
      }
      steps {
        unstash 'App'
        sh '''pwd
ls -la
ls -la ./build/libs/
cp ./build/libs/*.war ./docker
cd ./docker
pwd
ls -la
'''
        sh '''cd ./docker
pwd
ls -la
docker build -t webapp1:latest .
docker images
docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
docker push webapp1:latest'''
      }
    }
    stage('') {
      steps {
        script {
          withCredentials([usernameColonPassword(credentialsId: 'mylogin', variable: 'USERPASS')]) {
            sh '''
set +x
curl -u "$USERPASS" https://private.server/ > output
'''
          }
        }

      }
    }
  }
}