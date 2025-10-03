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
                # Workspace ला write permission दे
                chmod -R 777 $WORKSPACE

                # Virtual environment तयार करा
                python3 -m venv venv

                # Virtual environment activate करा
                . venv/bin/activate

                # pip upgrade करा
                python -m pip install --upgrade pip

                # requirements.txt install करा ( --user वापरायचं नाही कारण venv मध्येच install होईल)
                pip install -r requirements.txt

                echo "Dependencies installed successfully!"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                # Virtual environment activate करा
                . venv/bin/activate

                # App deploy command
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
