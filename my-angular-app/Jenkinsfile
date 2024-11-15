pipeline {
    agent any
    environment {
        NODEJS_HOME = tool name: 'NodeJS' // Use your configured Node.js tool in Jenkins
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/atharvalavangare/project.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('my-angular-app') { // Navigate to the Angular app folder
                    sh 'npm install'
                }
            }
        }
        stage('Build Angular App') {
            steps {
                dir('my-angular-app') { // Stay inside the Angular app folder
                    sh 'npm run build --prod'
                }
            }
        }
        stage('Deploy to Nginx') {
            steps {
                // Copy the build files to the Nginx deployment folder
                sh 'sudo cp -r my-angular-app/dist/my-angular-app/* /var/www/angular-app/'
                sh 'sudo systemctl reload nginx'
            }
        }
    }
    triggers {
        // Trigger on push to main branch
        githubPush()
    }
}