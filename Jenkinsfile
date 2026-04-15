pipeline {
    agent any

    stages {

        stage('Build & Test') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r app/requirements.txt pytest
                    pytest tests/
                '''
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Deploy Local') {
            steps {
                sh 'docker-compose up -d'
                echo "funcionando en http://localhost:5000"
            }
        }
    }
}
