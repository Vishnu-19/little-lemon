pipeline {
    agent any

    environment {
        NODE_VERSION = '18.17.1' // Set Node.js version manually
        NVM_DIR = "${HOME}/.nvm"
    }

    stages {

        stage('Set Up Node.js') {
            steps {
                sh '''
                    # Ensure NVM is available
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                    
                    # Install and use Node.js
                    nvm install ${NODE_VERSION}
                    nvm use ${NODE_VERSION}

                    # Verify node and npm are working
                    node -v
                    npm -v
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'React app build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
