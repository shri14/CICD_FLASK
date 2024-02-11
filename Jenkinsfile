pipeline {
    agent any

    environment {
        FLASK_APP = 'app.py'
        FLASK_ENV = 'test'
        PATH_TO_PYTHON = '/usr/bin/python3'
        PATH_TO_PIP = '/usr/bin/pip3'
    }

    // stages {
    //     stage('Checkout') {
    //         steps {
    //             script {
    //                 git 'https://github.com/shri14/CICD_FLASK.git'
    //             }
    //         }
    //     }

        stage('Update Werkzeug') {
            steps {
                script {
                    sh "${PATH_TO_PIP} install --upgrade Werkzeug==2.0.1"
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    sh "${PATH_TO_PIP} install -r requirements.txt"
                }
            }
        }

        stage('Run tests') {
            steps {
                script {
                    sh "${PATH_TO_PYTHON} test_app.py"
                }
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    sh "${PATH_TO_PYTHON} app.py &"
                    echo 'Flask application is starting...'
                    sleep 10
                    echo 'Flask application is running at http://43.204.238.129:5000/'
                }
            }
        }

        stage('Declarative: Post Actions') {
            steps {
                script {
                    sh 'pkill -f "python3 app.py"'
                }
            }
            post {
                always {
                    script {
                        sleep 5
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
    }
}
