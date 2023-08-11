#!/bin/bash

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
                sh './venv/bin/python -m venv venv'
                sh 'source venv/bin/activate'
                
                // Install dependencies
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                sh './venv/bin/python tests.py'
            }
        }
        
        stage('Deploy') {
            steps {
                // Run the Flask app
                sh './venv/bin/python app.py'
            }
        }
    }
}
