pipeline {
    agent any

    tools {
        nodejs 'node-18'
    }

    environment {
        APP_ENV = 'dev'
    }

    stages {
        stage('Checkout') {
            steps {
                echo "📥 Checking out code..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Script') {
            steps {
                sh 'node index.js || echo "index.js not found, skipping..."'
            }
        }

        stage('Environment Info') {
            steps {
                echo "🔧 Running in environment: ${APP_ENV}"
                sh 'node -v'
                sh 'npm -v'
            }
        }
    }

    post {
        always {
            echo "✅ Build complete"
        }
    }
}

