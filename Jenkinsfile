pipeline {
    agent any

    stages {
        stage('Fetch Data') {
            steps {
                git branch: 'main', url: 'https://github.com/shuja782/devops_mid.git'
            }
        }

        stage('Train Model') {
            steps {
                sh 'cp configs/FA23-BAI-040_config.json config.json'
                sh 'python3 train.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ml-api .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop ml-container || true'
                sh 'docker rm ml-container || true'
                sh 'docker run -d -p 8000:8000 --name ml-container ml-api'
            }
        }
    }
}
