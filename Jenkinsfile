pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'python3 -m pip install virtualenv'
                    sh 'python3 -m virtualenv venv'
                    sh 'source venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'python -m unittest discover'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    sh 'source venv/bin/activate && python app.py &'
                }
            }
        }
    }

    post {
        always {
            script {
                // Clean up: stop the Flask app
                sh 'pkill -f "python app.py"'
            }
        }
        success {
            echo 'Pipeline succeeded! Trigger further actions here.'
        }
        failure {
            echo 'Pipeline failed! Notify or take corrective actions.'
        }
    }
}
