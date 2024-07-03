pipeline {
    agent any
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
                    npm install --legacy-peer-deps
                    npm run build
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