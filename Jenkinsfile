pipeline {
    agent any

    stages {
        stage('Build') {
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
