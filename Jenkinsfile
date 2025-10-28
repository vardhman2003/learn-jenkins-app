pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh'''
                    ls -la 
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }

        stage('Test'){
            steps{
                if(sh(script: 'test -f /workspaces/learn-jenkins-app/build/index.html', returnStatus: true)==0){
                    echo 'File Exists'
                }
                else{
                    echo 'File does not exist'
                }
            }
        }
    }
}
