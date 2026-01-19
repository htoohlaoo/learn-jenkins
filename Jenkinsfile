pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node-18-alpine'
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
                '''
            }
        }
    }
}
