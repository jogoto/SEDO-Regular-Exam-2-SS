pipeline {
    agent any
    
    environment {
        DOTNET_VERSION = '8.0.x'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Setup .NET') {
            steps {
                script {
                    // Install .NET SDK if not already installed
                    def dotnetHome = tool name: 'dotnet-sdk-8.0', type: 'hudson.plugins.dotnet.DotNetInstallation'
                    env.PATH = "${dotnetHome}/bin:${env.PATH}"
                }
            }
        }
        
        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }
        
        stage('Build') {
            steps {
                sh 'dotnet build --no-restore --configuration Release'
            }
        }
        
        stage('Test') {
            steps {
                sh 'dotnet test --no-build --verbosity normal --configuration Release'
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
} 