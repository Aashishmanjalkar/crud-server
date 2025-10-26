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
                sudo npm install -g pm2
                sudo pm2 delete all || true
                sudo pm2 start server.js --name backend
                sudo pm2 save
                '''
            }
        }
    }
}
