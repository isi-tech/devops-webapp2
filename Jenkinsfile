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
    stage('Package') {
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
docker build -t cloudacademydevops/webapp1-2019:$BUILD_ID .
docker images
'''
      }
    }
    stage('Publish') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'ca-dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
            sh '''
docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
docker push cloudacademydevops/webapp1-2019:$BUILD_ID
'''
          }
        }

      }
    }
  }
}