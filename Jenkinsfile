
pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ishita2403/sentiment-app.git'
            }
        }

        stage('Sentiment Test Suite') {
            steps {
                sh '''
                    echo "Running Sentiment Test Suite"
                    grep -q "^BATCH=500$" sentiment.properties
                    echo "Configuration test passed!"
                '''
            }
        }

        stage('Package Container') {
            steps {
                sh '''
                    echo "Preparing Sentiment Worker package"
                    mkdir -p dist
                    cp sentiment.properties dist/
                    tar -czf sentiment-worker.tar.gz -C dist .
                    echo "Package created successfully!"
                '''

                archiveArtifacts artifacts: 'sentiment-worker.tar.gz',
                                 fingerprint: true
            }
        }
    }
}
