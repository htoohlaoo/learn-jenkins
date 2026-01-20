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
                echo 'building started...'
                sh '''
                    ls -al 
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls build | grep "index.html"
                '''
            }
        }
        stage("Test"){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo "test stage..."
                sh '''
                    ls -al 
                    test -f build/index.html
                    npm test
                '''
            }
            
        }
        stage("E2E"){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                echo "e2e test stage..."
                sh '''
                    npm install serve
                    nodemodules/serve -s build &
                    sleep 10
                    npx playwright test --reporter=html
                '''
            }
            
        }
        
    }
    post {
        always {
            junit "jest-results/junit.xml"
        }
    }
}
