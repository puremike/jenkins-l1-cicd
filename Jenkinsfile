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

        stage('E2E-Test') {
            agent {
                docker {
                    image "mcr.microsoft.com/playwright:v1.45.1-jammy"
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node_modules/.bin/serve -s build &
                    sleep 20
                    npx playwright test --reporter=html
                '''
            }
        }

    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }

        always {
            junit "test-results/junit.xml"
        }
    }
}