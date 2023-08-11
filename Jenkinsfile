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
                    // Set up your virtual environment
                    script {
                        sh '/usr/bin/python3 -m venv venv'
                        sh 'source venv/bin/activate'
                    }
                    
                    // Install dependencies
                    sh 'usr/bin/pip install -r requirements.txt'
                }
            }
            
            stage('Test') {
                steps {
                    // Run tests
                    sh '/usr/bin/python3 tests.py'
                }
            }
            
            stage('Deploy') {
                steps {
                    // Run the Flask app
                    sh '/usr/bin/python3 app.py'
                }
            }

    }
}
