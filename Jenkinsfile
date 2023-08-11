pipeline {
    agent any
    
    stages {
        stage('Check Python') {
            steps {
                script {
                    def pythonTool = 'Python3'
                    def pythonVersion = '3.8'
                    def pythonInstalled = tool name: pythonTool, type: 'hudson.plugins.python.PythonInstaller'
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
                script {
                    def pythonTool = 'Python3'
                    def pythonVersion = '3.8'
                    def pythonPath = tool name: pythonTool, type: 'hudson.plugins.python.PythonInstaller'
                    sh "${pythonPath}/bin/python3 -m venv venv"
                }
                sh 'source venv/bin/activate'
                
                // Install dependencies
                sh 'pip install -r requirements.txt'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                script {
                    def pythonTool = 'Python3'
                    def pythonPath = tool name: pythonTool, type: 'hudson.plugins.python.PythonInstaller'
                    sh "${pythonPath}/bin/python3 tests.py"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Run the Flask app
                script {
                    def pythonTool = 'Python3'
                    def pythonPath = tool name: pythonTool, type: 'hudson.plugins.python.PythonInstaller'
                    sh "${pythonPath}/bin/python3 app.py"
                }
            }
        }
    }
}
