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
                    echo "Building Application..."
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
                    echo "Test stage running..."
                    # The build/index.html file should be found in the mounted workspace directory:
                    test -f build/index.html
                    # Since we are using a Docker image, npm should be found and run:
                    npm test
                    echo "Test stage done"
                '''
            }
        }
    }
}
