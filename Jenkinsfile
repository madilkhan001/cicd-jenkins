pipeline {
  agent any
  stages {
    stage('git checkout') {
      steps {
        git(url: 'https://github.com/adilkhan0011/cicd-jenkins.git', branch: 'master')
      }
    }

    stage('Log') {
      steps {
        sh '''pwd
ls'''
      }
    }

    stage('build the images') {
      steps {
        sh '''docker build -f Dockerfile.mongo -t adilpriv/mongo:latest .
docker build -f Dockerfile.node -t adilpriv/node-app:latest .'''
      }
    }

    stage('docker login') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'dockerhub_id', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
            echo "Username: $USERNAME"
            echo "Password: $PASSWORD"
            // Use $USERNAME and $PASSWORD in your pipeline steps
            sh "docker login -u $USERNAME -p $PASSWORD"
          }
        }

      }
    }

    stage('push image to dockerhub') {
      steps {
        sh '''docker push/adilpriv/node-app:latest
docker push/adilpriv/mongo:latest'''
      }
    }

  }
}