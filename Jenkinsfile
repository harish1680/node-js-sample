pipeline {
    agent any

    tools {
        nodejs 'node-18'
    }

    environment {
        STAGE = 'dev'
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
                echo "Deploying to $STAGE environment"
            }
        }
    }
}

