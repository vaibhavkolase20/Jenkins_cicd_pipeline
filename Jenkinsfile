pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
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

                # Virtual environment activate करा
                source venv/bin/activate

                # pip upgrade करा
                pip install --upgrade pip

                # requirements.txt install करा
                pip install -r requirements.txt

                # जर आवश्यक असेल तर test command चालवा
                # python -m unittest discover tests
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

