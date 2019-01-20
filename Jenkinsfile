pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/jeremycook123/devops-webapp2/', branch: 'master')
      }
    }
    stage('Compile') {
      parallel {
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
        stage('Parallel1') {
          steps {
            sh '''date
echo run in parallel1'''
          }
        }
        stage('Parallel2') {
          steps {
            sh '''date
echo run in parallel2
pwd
ls -la'''
          }
        }
      }
    }
    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
    }
  }
}