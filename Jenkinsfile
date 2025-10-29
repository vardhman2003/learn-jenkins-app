pipeline {
    agent any

    stages {
        // stage('Build') {
        //     agent{
        //         docker{
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh'''
        //             ls -la 
        //             node --version
        //             npm --version
        //             npm ci
        //             npm run build
        //             ls -la
        //         '''
        //     }
        // }

        stage('Test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh''' 
                    test -f  build/index.html
                    npm test
                '''
                    
            }
        }
        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.41.1'
                    reuseNode true
                    
                }
            }
            steps{
                sh''' 
                    npm install serve
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test --reporter=html
                '''
                    
            }
        }
    }
//     post{
//         always{
//             junit 'jest-results/junit.xml'
//         }
//     stage('E2E') {
//         agent {
//             docker {
//                 image 'mcr.microsoft.com/playwright:v1.41.1'
//                 reuseNode true
//             }
//         }
//         steps {
//             sh '''
//                 # Install serve if not already present
//                 npm install serve

//                 # Start the build server in the background
//                 nohup node_modules/.bin/serve -s build --listen 3000 > /dev/null 2>&1 &
// 5
//                 # Wait for the server to be ready
//                 echo "Waiting for server to start..."
//                 for i in {1..10}; do
//                 curl -s http://localhost:3000 > /dev/null && break
//                 sleep 2
//                 done

//                 # Run Playwright tests
//                 npx playwright test

//                 # Optional: kill the server after tests
//                 pkill -f "serve"
//         '''
//     }
// }

//     }
}
