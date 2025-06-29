pipeline {
    agent any
    
    environment {
        DOTNET_VERSION = '8.0.x'
        DOTNET_PATH = '/home/sstanchev/.dotnet/dotnet'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Restore Dependencies') {
            steps {
                sh "${DOTNET_PATH} restore"
            }
        }
        
        stage('Build') {
            steps {
                sh "${DOTNET_PATH} build --no-restore --configuration Release"
            }
        }
        
        stage('Test') {
            steps {
                sh "${DOTNET_PATH} test --no-build --verbosity normal --configuration Release"
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