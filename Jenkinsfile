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
                   
                    sh 'sudo apt-get update -y'

                    sh 'sudo apt-get install -y python3-venv'
                    sh 'python3 -m venv venv'
                }
            }
        }

        stage('Run Tests') {
            when {
                expression {
                    
                    return env.BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    // Add steps to run tests
                    sh 'pytest'
                }
            }
        }

        stage('Run Application') {
            when {
                expression {
                    // Specify the condition for running this stage
                    // For example, run application for branches other than 'main'
                    return env.BRANCH_NAME != 'master'
                }
            }
            steps {
                script {
                    // Add steps to run the application
                    sh 'python app.py &'
                }
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
