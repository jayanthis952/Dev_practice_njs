pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t my-app:v1 -f my-app/Dockerfile my-app'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push jayanthim/my-app:v1'
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
}
