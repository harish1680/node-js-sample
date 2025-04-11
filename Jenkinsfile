pipeline {
    agent any

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

        stage('Build & Deploy Docker Container') {
            steps {
                sh '''
                    docker stop nodejs-docker-demo || true
                    docker rm nodejs-docker-demo || true
                    docker build -t node-js-sample .
                    docker run -d -p 5000:5000 \
                        --name nodejs-docker-demo \
                        -e PORT=$PORT \
                        -e API_KEY=$API_KEY \
                        node-js-sample
                '''
            }
        }
    }
}

