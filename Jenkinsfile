pipeline {
    agent any

    triggers {
        // Schedule: run every 2 minutes (CRON syntax)
        cron('H/2 * * * *')
        // Optional: webhook trigger from GitHub
    }

    environment {
        GIT_URL = 'https://github.com/farhaghallab3/iti-python-10-2025.git'
        GIT_BRANCH = 'main'
        GIT_CREDENTIALS = 'github-path'  // اسم الـ credential اللي أضفناه في Jenkins
    }

    stages {

        stage('Clone from GitHub') {
            steps {
                git branch: "${env.GIT_BRANCH}", credentialsId: "${env.GIT_CREDENTIALS}", url: "${env.GIT_URL}"
            }
        }

        stage('Build') {
    steps {
        echo "Building and running Python app inside container..."
        sh '''
        docker run --rm -v "$PWD":/app -w /app python:3.10-slim python app.py
        '''
    }
}


        stage('Deploy (Optional)') {
            steps {
                echo "Deploying with Docker (if Dockerfile exists)..."
                sh '''
                if [ -f Dockerfile ]; then
                    docker build -t iti-python-app .
                    docker run --rm iti-python-app
                else
                    echo "No Dockerfile found, skipping container build."
                fi
                '''
            }
        }
    }

    post {
        always {
            echo "Cleaning workspace..."
            cleanWs()
        }
    }
}
