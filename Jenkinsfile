pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'source', url:'https://github.com/GACQUADRO/integration.git'
            }
        }
        stage('Build backend') {
            agent {
                label 'docker-agent-python'
            }
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}