pipeline {
    agent any

    environment {
         NODEJS_HOME = tool 'NodeJS_20' // Define Node.js installation
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', credentialsId: '7abbb7c9-c1f8-433b-b2d7-9c75b36fbfad', url: 'https://github.com/VaishnaviGaidhane/frontend_project.git'
            }
        }

        stage('Install Dependencies') {
    steps {
        script {
            def nodejs = tool name: 'NodeJS_20', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
            env.PATH = "C:\Program Files\nodejs\node.exe"
        }
        bat 'npm install'
    }
}

        stage('Linting') {
            steps {
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
