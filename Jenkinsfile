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
                    echo "📂 Listing files..."
                    ls -la

                    echo "🟢 Node version:"
                    node --version

                    echo "📦 NPM version:"
                    npm --version

                    echo "📥 Installing dependencies..."
                    npm ci

                    echo "🏗️ Building project..."
                    npm run build

                    echo "📂 Listing files..."
                    ls -la
                '''
            }
        }
    }
}
