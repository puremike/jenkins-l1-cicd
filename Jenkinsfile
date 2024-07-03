pipeline {
    agent any
    environment {
        HOME = "."
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image "node:alpine3.20"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image "node:alpine3.20"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Test Stage"
                    test -f build/index.html
                    npm test
                '''
            }
        }

    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}