pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Check if Python is installed
                    def pythonInstalled = sh(script: 'command -v python', returnStatus: true) == 0

                    // Install Python if not present
                    if (!pythonInstalled) {
                        sh 'sudo apt-get update -y'
                        sh 'sudo apt-get install python3 -y'
                    }

                    // Set up your virtual environment
                    sh 'python -m venv venv'
                    sh 'source venv/bin/activate'

                    // Install dependencies
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                sh 'python tests.py'
            }
        }
        
        stage('Deploy') {
            steps {
                // Run the Flask app
                sh 'python app.py'
            }
        }
    }
}
