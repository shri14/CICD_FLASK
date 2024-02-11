pipeline {
    agent any

    environment {
        FLASK_APP = 'app.py'
        FLASK_ENV = 'test'
    }

    tools {
        // Assuming Python3 is configured in Jenkins
        python 'Python3'
    }

    stages {
        stage('Install dependencies') {
            steps {
                script {
                    // Upgrade pip
                    sh 'python -m pip install --upgrade pip'

                    // Install dependencies
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Run tests') {
            steps {
                script {
                    sh 'python test_app.py'
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    sh 'python app.py &'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'pkill -f "python app.py"'
            }
        }

        success {
            echo 'Pipeline succeeded! Deploy your application.'
        }

        failure {
            echo 'Pipeline failed! Check the build logs.'
        }
    }
}
