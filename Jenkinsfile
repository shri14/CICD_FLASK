pipeline {
    agent any // Use any available node

    environment {
        // Define any necessary environment variables for your app
        FLASK_APP = "app.py" // Replace with your Flask app's entry point
        VIRTUALENV_DIR = ".venv" // Replace with your desired virtual environment name
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'your_git_repository_url', credentialsId: 'your_credentials_id'
            }
        }

        // Step 2: Install dependencies using virtual environment
        stage('Install Dependencies') {
            steps {
                sh 'python3 -m venv ${VIRTUALENV_DIR}' // Create virtual environment
                sh 'source ${VIRTUALENV_DIR}/bin/activate' // Activate virtual environment
                sh 'pip install -r requirements.txt' // Install dependencies
            }
        }

        // Step 3: Run tests
        stage('Run Tests') {
            steps {
                sh 'source ${VIRTUALENV_DIR}/bin/activate' // Activate virtual environment
                sh 'nosetests test_app.py' // Or your chosen test runner
            }
        }

        // Step 4: Build the app (customize or remove if not applicable)
        stage('Build App') {
            when {
                expression { branch == 'master' || branch == 'release' } // Only build on certain branches
            }
            steps {
                sh 'source ${VIRTUALENV_DIR}/bin/activate' // Activate virtual environment
                sh 'python ${FLASK_APP} build' // Or your build command
            }
        }

        // Step 5: Deploy the app (optional, customize based on deployment strategy)
        stage('Deploy to Production') {
            when {
                expression { branch == 'master' } // Only deploy on the main branch
            }
            steps {
                // Replace with your deployment commands/steps
                // Example: upload artifact to a server, run a script on a deployment server, etc.
            }
        }
    }

    // Step 6: Post-build actions (optional, add as needed)
    post {
        success {
            archiveArtifacts 'dist/*' // Optionally archive build artifacts
        }
        failure {
            // Send notifications, etc.
        }
    }
}
