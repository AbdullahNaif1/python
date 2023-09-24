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
                 withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                     sh 'docker login -u $USERNAME -p $PASSWORD'
                     sh 'docker tag my_app:latest <dockerhub_username>/my_app:latest'
                     sh 'docker push <dockerhub_username>/my_app:latest'
                 }
             }
         }
         stage('Deploy') {
             steps {
                 sh 'ssh <your_server> "docker pull <dockerhub_username>/my_app:latest && docker run -d -p 80:5000 <dockerhub_username>/my_app:latest"'
             }
         }
     }
 }
