pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaysanghani19/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' 
            }
            post {
                always {
                    emailext attachLog: true, 
                             subject: "Jenkins Pipeline: Run Tests Stage", 
                             body: "The 'Run Tests' stage has finished executing. Please review the attached log file for the status (success or failure).", 
                             to: "your-email@example.com"
                }
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0' 
            }
            post {
                always {
                    emailext attachLog: true, 
                             subject: "Jenkins Pipeline: Security Scan Stage", 
                             body: "The 'Security Scan' stage has finished executing. Please review the attached log file for vulnerability details.", 
                             to: "your-email@example.com"
                }
            }
        }
    }
}
