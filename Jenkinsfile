pipeline {
    agent any

    environment {
        HOME = pwd()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install python3-venv package
                    sh 'apt-get update'
                    sh 'apt-get install -y python3-venv'

                    // Set up virtual environment
                    sh 'python3 -m venv venv'
                    sh 'source venv/bin/activate && pip install -r requirements.txt'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'source venv/bin/activate && python -m unittest discover'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    // Start the Flask app in the background
                    sh 'source venv/bin/activate && nohup python app.py > /dev/null 2>&1 &'
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
