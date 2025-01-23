pipeline {
    agent any

    environment {
        NODEJS_HOME = tool 'NodeJS' // Define Node.js installation
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', credentialsId: '7abbb7c9-c1f8-433b-b2d7-9c75b36fbfad', url: 'https://github.com/yourusername/frontend-project.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // If using npm, otherwise ignore for pure HTML/CSS/JS
            }
        }

        stage('Linting') {
            steps {
                sh 'npx eslint "**/*.js" || true'
                sh 'npx stylelint "**/*.css" || true'
            }
        }

        stage('Build') {
            steps {
                echo 'No build step required for static site'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
                sh 'scp -r ./* user@server-ip:/var/www/html/'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}
