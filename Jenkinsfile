pipeline {
    agent any

    environment {
        NODE_VERSION = '18'  // Set Node.js version
    }

    stages {

        stage('Set Up Node.js') {
            steps {
                script {
                    // Use Node.js version from environment variable
                    def node_version = NODE_VERSION
                    sh "nvm install ${node_version} && nvm use ${node_version}"
                }
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
