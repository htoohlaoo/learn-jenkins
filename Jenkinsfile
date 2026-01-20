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
        
    }
    post {
        always {
            junit "test-results/junit.xml"
        }
    }
}
