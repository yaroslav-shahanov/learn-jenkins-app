pipeline {
    agent any

    stages {
        stage('without docker') {
            steps {
                echo 'without docker'
                sh 'touch container-no.txt'
            }
        }
        stage('with docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh 'echo "With docker"'
                sh 'ls -la'
                sh 'touch container-yes.txt'
            }
        }
    }
}
