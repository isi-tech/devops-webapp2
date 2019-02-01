pipeline {
  agent {
    node {
      label 'agent1'
    }

  }
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2', branch: 'master')
      }
    }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
            stash(name: 'App', includes: 'build/libs/*.war')
          }
        }
        stage('P1') {
          steps {
            sh '''date
echo run parallel!!'''
          }
        }
        stage('P2') {
          steps {
            sh '''date
echo run parallel!!'''
          }
        }
      }
    }
    stage('Package') {
      steps {
        unstash 'App'
        sh '''ls -la ./build/libs/
cp ./build/libs/*.war ./docker
cd ./docker
ls -la'''
        sh '''cd ./docker
ls -la
docker build -t cloudacademydevops/webapp1-2019:$BUILD_ID .
docker tag cloudacademydevops/webapp1-2019:$BUILD_ID cloudacademydevops/webapp1-2019:latest
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
docker push cloudacademydevops/webapp1-2019:latest
'''
          }
        }

      }
    }
  }
}