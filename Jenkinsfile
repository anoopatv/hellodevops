pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('Build & Package') {
            steps {
                sh '''
                mkdir -p build
                tar -czf build/hello-devops.tar.gz app.py requirements.txt
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/*.tar.gz', fingerprint: true
        }
    }
}
