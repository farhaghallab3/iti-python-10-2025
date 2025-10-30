echo "pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        echo 'Cloning from GitHub...'
      }
    }
    stage('Build') {
      steps {
        echo 'Building the app...'
        sh 'python app.py'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploy stage...'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}" > Jenkinsfile
