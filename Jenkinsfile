pipeline {
    agent any

    stages {
        stage('Clone from GitHub') {
            steps {
                git url: 'https://github.com/farhaghallab3/iti-python-10-2025.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building and running Python app...'
                sh 'python3 app.py'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
    }
}
