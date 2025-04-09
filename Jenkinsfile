pipeline {
    agent any

    tools {
        nodejs 'node-18'  // Make sure this is configured in Jenkins global tools
    }

    environment {
        PORT = credentials('PORT')              // Make sure these credentials exist in Jenkins
        API_KEY = credentials('MY_SECRET_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/harish1680/node-js-sample.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'npm test -- --passWithNoTests' // In case no tests exist (optional)
            }
        }

        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    pm2 delete node-js-sample || true
                    pm2 start index.js --name node-js-sample
                '''
            }
        }
    }

    post {
        always {
            junit 'test-reports/junit.xml'
        }
    }
}

