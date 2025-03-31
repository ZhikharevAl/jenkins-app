pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u 103:110'
                }
            }
            steps {
                sh """
                    set -e
                    rm -rf node_modules
                    export NPM_CONFIG_CACHE=/var/lib/jenkins/workspace/jenkins-app/npm-cache
                    npm cache clean --force
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                """
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }
}