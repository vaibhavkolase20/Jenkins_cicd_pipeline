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

        stage('Build') {
            steps {
                sh 'echo Building Hello World App'
            }
        }

        stage('Test') {
            steps {
                sh '''
                # Virtual environment तयार करा
                python3 -m venv venv

                # Virtual environment activate करा (POSIX shell compatible)
                . venv/bin/activate

                # pip upgrade करा
                pip install --upgrade pip

                # requirements.txt install करा
                pip install -r requirements.txt

                # Test commands (जर आवश्यक असेल तर)
                # python -m unittest discover tests
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                # Virtual environment activate करा
                . venv/bin/activate

                # App deploy command (उदाहरणार्थ)
                # python app.py
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

