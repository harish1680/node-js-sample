pipeline {
    agent any

    tools {
        nodejs 'node-18'
    }

    environment {
       PORT = credentials('PORT')
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
                sh 'npm test'
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
                    pm2 delete all || true
                    pm2 start index.js --name node-js-sample
                '''
	         }
        }
    }
}

