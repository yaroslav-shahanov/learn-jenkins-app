pipeline {
    agent any

    stages {
        // stage('Build') {
        //     agent { 
        //         docker { 
        //             image 'node:18-alpine' 
        //             reuseNode true 
        //             } 
        //         }
        //     steps {
        //         sh '''
        //            ls -la
        //            node --version
        //            npm --version
        //            npm ci
        //            npm run build 
        //            ls -la
        //            '''
        //     }
        // }

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
        stage('E2E') {
            agent { 
                docker { 
                    image 'mrc.microsoft.com/playright:v1.39.0-jammy' 
                    reuseNode true 
                    args '-u root:root'
                    } 
                }
            steps {
                sh '''
                   npm install -g serve
                   serve -s build
                   npx playright test
                   '''
            }
        
        }
    }

    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}
