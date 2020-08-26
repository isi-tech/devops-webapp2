pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/isi-tech/devops-webapp2', branch: 'master')
      }
    }

    stage('build') {
      parallel {
        stage('build') {
          steps {
            sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
          }
        }

        stage('p1') {
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

    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}