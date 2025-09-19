pipeline {
    agent any
    tools { nodejs 'node18' }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/prashantdeakin/8.2CDevSecOps.git'
            }
        }
        stage('Check Node') {
            steps {
                sh 'echo PATH=$PATH'
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }
}
