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

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true 
                }
            }
            steps {
                sh '''
                    echo "✅ Checking if build/index.html exists..."
                    if [ -f build/index.html ]; then
                        echo "✔ build/index.html found"
                    else
                        echo "❌ build/index.html missing" && exit 1
                    fi

                    echo "🧪 Running unit tests..."
                    npm test -- --ci --reporters=default --reporters=jest-junit
                '''
            }
        }
    }
}
