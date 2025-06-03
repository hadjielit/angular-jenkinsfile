pipeline {
    agent any

    tools {
        // Configure Node.js 24.1.0 in Jenkins:
        // Manage Jenkins > Global Tool Configuration > NodeJS installations
        nodejs 'nodejs-24.1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Angular') {
            steps {
                sh 'npm run build -- --configuration=production'
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'npm test -- --watch=false --browsers=ChromeHeadless'
                junit 'test-results.xml' // Assumes Karma is configured to output JUnit format
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dist/**/*', allowEmptyArchive: true
            cleanWs()
        }
    }
}
