pipeline {
      agent any
      stages {
          stage('Checkout') {
              steps {
                  checkout scm
              }
          }
          stage('Build Docker Image') {
              steps {
                  sh 'docker build -t my_app .'
              }
          }
          stage('Push Docker Image') {
              steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                      sh 'docker login -u $USERNAME -p $PASSWORD'
                      sh 'docker tag my_app:latest abdullah919191/my_app:latest'
                      sh 'docker push abdullah919191/my_app:latest'
                  }
              }
          }
          stage('Deploy') {
              steps {
                  sh 'docker pull abdullah919191/my_app:latest && docker run -d -p 8083:5000 abdullah919191/my_app:latest'
              }
          }
      }
  }
