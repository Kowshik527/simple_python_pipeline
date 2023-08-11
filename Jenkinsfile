pipeline {
    agent any
    
    stages {
        stage('Check Python') {
            steps {
                script {
                    def pythonInstalled = tool(name: 'Python', type: 'hudson.plugins.python.PythonInstaller') {
                        installations {
                            'Python3': '3.8' // Change this to the version you need
                        }
                    }
                    if (!pythonInstalled) {
                        error('Python is not installed. Please configure Python tool in Jenkins settings.')
                    }
                }
            }
        }
        
        stage('Checkout') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Set up your virtual environment
                sh "${tool name: 'Python3', type: 'hudson.plugins.python.PythonInstaller'}/bin/python3 -m venv venv"
                sh 'source venv/bin/activate'
                
                // Install dependencies
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                sh "${tool name: 'Python3', type: 'hudson.plugins.python.PythonInstaller'}/bin/python3 tests.py"
            }
        }
        
        stage('Deploy') {
            steps {
                // Run the Flask app
                sh "${tool name: 'Python3', type: 'hudson.plugins.python.PythonInstaller'}/bin/python3 app.py"
            }
        }
    }
}
