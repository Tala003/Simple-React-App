pipeline {
    agent any

    environment {
        # Add your Vercel token here in Jenkins credentials or as plain text
        VERCEL_TOKEN = credentials('vercel-token')

    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/your-username/your-react-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node modules
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                // Build React project
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                // Deploy build folder to Vercel
                sh """
                npx vercel --token $VERCEL_TOKEN --prod --confirm \
                --name $VERCEL_PROJECT_NAME --org $VERCEL_ORG_ID
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
