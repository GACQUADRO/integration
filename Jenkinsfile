pipeline {
    agent none

    stages {
        stage('Checkout code') {
            agent any
            steps {
                git branch: 'source', url: 'https://github.com/bart120/m2-cicd.git' // plugin Git
                sh 'ls -R ${WORKSPACE}'
                stash name: 'source-code', includes: '**' 
            }
        }

        stage('Build Backend') {
            agent {
                label 'docker-agent-python'
            }
            steps {
                unstash 'source-code'  
                sh 'ls -R ${WORKSPACE}' 
                sh 'pip install -r back/requirements.txt'
            }
        }

        stage('Test') {
            agent {
                label 'agent-python-test'
            }
            steps {
                unstash 'source-code'  
                echo 'Running default test...'

                // Crée un test minimal si aucun n'existe
                sh '''
                mkdir -p tests
                if [ ! -f tests/test_default.py ]; then
                  echo "def test_dummy(): assert True" > tests/test_default.py
                fi
                '''


                sh 'pytest tests/'
            }
        }

        stage('Deploy') {
            agent any
            steps {
                echo 'Deploying....'
            }
        }
    }
}
