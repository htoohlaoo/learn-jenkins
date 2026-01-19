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
                cleanWs()
                echo 'building started...'
                sh '''
                    ls -al 
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls build | grep "index.html"
                '''
                echo 'testing started...'
                sh '''
                    ls build | grep "index.html"
                    npm test
                '''
            }
        }
        
    }
}
