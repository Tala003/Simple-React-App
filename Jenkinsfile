
pipeline {
    agent any

    environment {
        // Add your Vercel token here in Jenkins credentials or as plain text
      VERCEL_TOKEN = credentials('vercel-token')

    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Tala003/Simple-React-App.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                sh """
                npx vercel --token $VERCEL_TOKEN --prod --confirm \
                """
            }
        }
    }

    post {
        success {
            echo 'React app deployed successfully to Vercel!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}

