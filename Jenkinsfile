pipeline {
    agent any

    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'sudo apt-get update -y'
                sh 'sudo apt-get install -y python3-venv'
                sh 'python3 -m venv venv'
            }
        }

        stage('Run Tests') {
            when {
                expression {
                    // Replace 'your_condition_here' with your actual condition
                    true
                }
            }
            steps {
                script {
                    // Your test execution steps here
                    // For example: sh 'pytest'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    // Your application execution steps here
                    // For example: sh 'python app.py'
                }
            }
        }

        stage('Declarative: Post Actions') {
            post {
                always {
                    script {
                        // Your post-action steps here
                        // For example: sh 'pkill -f python app.py'
                    }
                }
            }
        }
    }
}
