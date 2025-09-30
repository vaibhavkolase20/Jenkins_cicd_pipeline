pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Building Hello World App"'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pip install -r requirements.txt'
                sh 'python3 -m pytest test_app.py'
            }
        }
    }
}

