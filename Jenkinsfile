pipeline {
    agent any

    tools {
        nodejs 'NodeJS'  // Use the exact name configured in Jenkins settings
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/frontend-project.git'
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
