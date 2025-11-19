pipeline {
    agent any
    environment {
        VERCEL_TOKEN = credentials('vercel-token')
        
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run unit tests
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build the React application
                sh 'npm run build'
            }
        }

         stage('Archive Artifacts') {
            steps {
                // Archive the build artifacts
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Deploy the React application to Vercel
                sh "vercel --token $VERCEL_TOKEN --prod"
            }
        }
            }
        }
    

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
