pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/Aashishmanjalkar/crud-server'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || echo "No build step"'
            }
        }

        stage('Start app with PM2') {
            steps {
                sh '''
                npm install -g pm2
                pm2 delete all || true
                pm2 start server.js --name backend
                pm2 save
                '''
            }
        }
    }
}
