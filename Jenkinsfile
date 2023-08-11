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
        
        stage('Installing packages') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }
        stage('Static Code Checking') {
            steps {
                script {
                    sh 'find . -name \\*.py | xargs pylint -f parseable --output-format=pylint.log || true'
                    recordIssues(
                        tools: [pyLint(pattern: 'pylint.log')],
                        unstableTotalAll: 100
                    )
                }
            }
        }
        stage('Running Unit tests') {
            steps {
                script {
                    sh 'pytest --junitxml=pyunit.xml --cov-report xml:cov.xml tests/*.py || true'
                    step([$class: 'CoberturaPublisher', 
                        coberturaReportFile: "cov.xml",
                        onlyStable: false,
                        failNoReports: true,
                        failUnhealthy: false,
                        failUnstable: false,
                        autoUpdateHealth: true,
                        autoUpdateStability: true,
                        zoomCoverageChart: true,
                        maxNumberOfBuilds: 10,
                        lineCoverageTargets: '80, 80, 80',
                        conditionalCoverageTargets: '80, 80, 80',
                        classCoverageTargets: '80, 80, 80',
                        fileCoverageTargets: '80, 80, 80',
                    ])
                    junit "pyunit.xml"
                }
            }
        }
    }
}
