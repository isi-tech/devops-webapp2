pipeline {
  agent {
    node {
      label 'agent2'
    }

  }
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
./gradlew build
ls -la
ls -la build/libs/'''
        stash(name: 'App', includes: 'build/libs/*.war')
      }
    }
    stage('Docker') {
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
docker build -t jeremycookdev/webapp1-2019:$BUILD_ID .
docker images
'''
      }
    }
    stage('Auth') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
            sh '''
docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
docker push jeremycookdev/webapp1-2019:$BUILD_ID
'''
          }
        }

      }
    }
  }
}