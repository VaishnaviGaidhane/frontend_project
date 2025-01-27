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
                bat '"C:\\Program Files\\nodejs\\npm.cmd" install -g npx'
                bat ' "C:\\Program Files\\nodejs\\npm.cmd" install -g eslint stylelint'
                bat '"C:\\Program Files\\nodejs\\node.exe" -v'
                bat '"C:\\Program Files\\nodejs\\npm.cmd" exec -- "C:\\Program Files\\nodejs\\node.exe" eslint "/*.js" || exit 0'
                bat '"C:\\Program Files\\nodejs\\npm.cmd" exec -- "C:\\Program Files\\nodejs\\node.exe" stylelint "/*.css" || exit 0'
                
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
                 bat """
            robocopy . \\192.168.56.1\\var\\www\\html /MIR /Z /R:3 /W:5
        """

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
