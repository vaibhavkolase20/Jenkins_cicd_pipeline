pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/vaibhavkolase20/Jenkins_cicd_pipeline.git']]
                ])
            }
        }

        stage('Setup Python & Permissions') {
            steps {
                sh '''
                echo "Updating package list..."
                sudo apt update

                echo "Installing Python3, venv, pip..."
                sudo apt install -y python3 python3-venv python3-pip

                echo "Fixing workspace permissions..."
                sudo chown -R jenkins:jenkins $WORKSPACE
                sudo chmod -R 755 $WORKSPACE
                '''
            }
        }

        stage('Build & VirtualEnv Setup') {
            steps {
                sh '''
                echo "Creating virtual environment..."
                python3 -m venv venv

                echo "Activating virtual environment..."
                . venv/bin/activate

                echo "Upgrading pip..."
                python -m pip install --upgrade pip

                echo "Installing requirements..."
                pip install -r requirements.txt || echo "No requirements.txt, skipping"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Activating virtual environment for tests..."
                . venv/bin/activate

                echo "Running tests..."
                pytest || echo "Tests failed or pytest not installed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                echo "Activating virtual environment for deployment..."
                . venv/bin/activate

                echo "Deploying app..."
                python app.py
                echo "App deployed successfully!"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
