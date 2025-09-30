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
                sh 'pip install -r requirements.txt'
                sh 'pytest test_app.py'
            }
        }
    }
}

