pipeline {
    agent any

    environment {
         NODEJS_HOME = tool 'NodeJS_22' // Define Node.js installation
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', credentialsId: '7abbb7c9-c1f8-433b-b2d7-9c75b36fbfad', url: 'https://github.com/VaishnaviGaidhane/frontend_project.git'
            }
        }
   
        stage('Verify NodeJS Setup') {
            steps {
                bat '"C:\\Program Files\\nodejs\\node.exe" -v'
                bat '"C:\\Program Files\\nodejs\\npm.cmd" -v'
            }
        }
        
     stage('Install Dependencies') {
    steps {
    
        bat '"C:\\Program Files\\nodejs\\npm.cmd" install'
    }
}

        stage('Linting') {
            steps {
                bat 'npm install -g npx'
                bat 'npx eslint "**/*.js" || true'
                bat 'npx stylelint "**/*.css" || true'
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
                bat 'scp -r ./* user@server-ip:/var/www/html/'
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
