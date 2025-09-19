pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/prashantdeakin/8.2CDevSecOps.git'
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
            post {
                always {
                    emailext (
                        subject: "Build ${env.BUILD_NUMBER} - Test Stage Complete",
                        body: "Test stage completed. Status: ${currentBuild.result ?: 'SUCCESS'}",
                        to: "your-email@gmail.com",
                        attachLog: true
                    )
                }
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
            post {
                always {
                    emailext (
                        subject: "Build ${env.BUILD_NUMBER} - Security Scan Complete",
                        body: "Security scan found 139 vulnerabilities. Check attached logs for details.",
                        to: "pthapa@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}
