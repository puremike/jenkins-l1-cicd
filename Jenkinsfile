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
                cleanWs()
                sh '''
                    node --version
                    npm --version
                    npm ci
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