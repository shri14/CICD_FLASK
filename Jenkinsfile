pipeline {
    agent any

    environment {
        FLASK_APP = "app.py"
        VIRTUALENV_DIR = ".venv"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'your_git_repository_url', credentialsId: 'your_credentials_id'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv ${VIRTUALENV_DIR}
                    source ${VIRTUALENV_DIR}/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    source ${VIRTUALENV_DIR}/bin/activate
                    nosetests test_app.py
                '''
            }
        }

        stage('Build App') {
            when {
                expression { branch == 'main' || branch == 'release' }
            }
            steps {
                sh '''
                    source ${VIRTUALENV_DIR}/bin/activate
                    python ${FLASK_APP} build
                '''
            }
        }

        stage('Deploy to Production') {
            when {
                expression { branch == 'main' }
            }
            steps {
                // Replace with your deployment commands/steps
            }
        }
    }

    post {
        success {
            archiveArtifacts 'dist/*'
        }
        failure {
            // Send notifications, etc.
        }
    }
}
