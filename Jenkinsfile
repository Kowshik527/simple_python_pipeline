pipeline {
    agent any
    
    tools {
        // Define the tool installation for Python3
        python3 'Python3'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Set up your virtual environment
                script {
                    sh 'python3 -m venv venv'
                    sh 'source venv/bin/activate'
                }
                
                // Install dependencies
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                sh 'python3 tests.py'
            }
        }
        
        stage('Deploy') {
            steps {
                // Run the Flask app
                sh 'python3 app.py'
            }
        }
    }
}
