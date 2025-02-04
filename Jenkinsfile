pipeline {
    agent any

    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci 
                    npm run build 
                    ls -la 
                '''
            }
        }
        
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test                      
                '''
            }
        }

        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            environment {
                NETLIFY_ACCOUNT_ID = '67a1fdc2e6cde35c87f92ab5'  // Replace with your actual Netlify account ID
            }
            steps {
                sh '''
                    npm install netlify-cli
                    npx netlify --version
                    echo "Netlify Account ID: $NETLIFY_ACCOUNT_ID"
                '''
            }
        }
    }
}
