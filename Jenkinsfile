pipeline {
    agent any

    environment {
        HOME = '/var/lib/jenkins'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Update packages
                    sh 'apt-get update -y'

                    // Install dependencies or perform other necessary steps
                    // For example, install Python virtual environment
                    sh 'apt-get install -y python3-venv'
                    sh 'python3 -m venv venv'
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Add steps to run tests
            }
        }

        stage('Run Application') {
            steps {
                // Add steps to run the application
            }
        }
    }

    post {
        always {
            script {
                // Stop the application (if running)
                sh 'pkill -f python app.py'
            }
        }
    }
}
