pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/TU_USUARIO/mi-repositorio-devops.git'
            }
        }

        stage('Build & Test') {
            steps {
                // Instalamos dependencias y corremos el test (como pedía el buildspec)
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
                // Construimos la imagen localmente
                sh 'docker compose build'
            }
        }

        stage('Deploy Local') {
            steps {
                // Levantamos el contenedor
                sh 'docker compose up -d'
                echo "Construcción y despliegue finalizado con éxito en http://localhost:5000"
            }
        }
    }
}
