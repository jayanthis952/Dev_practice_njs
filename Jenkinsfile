pipeline {
  agent any

  environment {
    IMAGE_NAME = "jayanthim/my-app"
    TAG = "v1"
  }

  stages {

    stage('Checkout') {
      steps {
        git 'https://github.com/jayanthis952/Dev_practice_njs.git'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t $IMAGE_NAME:$TAG -f my-app/Dockerfile my-app'
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'docker-cred',
          usernameVariable: 'DOCKER_USER',
          passwordVariable: 'DOCKER_PASS'
        )]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
        }
      }
    }

    stage('Push') {
      steps {
        sh 'docker push $IMAGE_NAME:$TAG'
      }
    }

    stage('Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }

  }
}
