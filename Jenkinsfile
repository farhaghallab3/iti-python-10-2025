pipeline {
    agent any

    triggers {
      
        cron('H 10 * * *')
      
    }

    environment {
        APP_NAME = "iti-python-10-2025"
        REPO_URL = "https://github.com/farhaghallab3/iti-python-10-2025.git"
    }

    stages {
        stage('Clone from GitHub') {
            steps {
                echo "Cloning from ${REPO_URL}"
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build') {
            steps {
                echo "Building and running Python app..."
                sh '''
                if ! command -v python3 &> /dev/null
                then
                    echo "Python3 not found, installing..."
                    apt-get update && apt-get install -y python3 python3-pip
                fi
                python3 app.py
                '''
            }
        }

        stage('Docker Build & Run (Optional)') {
            when {
                expression { fileExists('Dockerfile') }
            }
            steps {
                echo "Dockerfile detected, building Docker image..."
                sh '''
                docker build -t ${APP_NAME}:latest .
                docker run -d -p 5000:5000 --name ${APP_NAME}_container ${APP_NAME}:latest || echo "Container may already exist"
                '''
            }
        }

        stage('Deploy (Simulated)') {
            steps {
                echo "Deploying app (simulated)..."
                echo "Deployment complete ✅"
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
