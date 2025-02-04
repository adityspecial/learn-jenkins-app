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
                NETLIFY_ACCOUNT_ID = 'e8f4dec0-a198-4a8f-9185-f786fdb3b2b9'  // Replace with your actual Netlify account ID
            }
            steps {
                sh '''
                    npm install -g netlify-cli
                    netlify --version
                    echo "Netlify Account ID: $NETLIFY_ACCOUNT_ID"
                '''
            }
        }
    }
}
