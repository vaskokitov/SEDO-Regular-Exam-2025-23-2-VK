pipeline {
    agent any

    environment {
        DOTNET_VERSION = '6.0.x'
    }

    stages {
        stage('Checkout Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Setup .NET') {
            steps {
                script {
                    sh 'wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb'
                    sh 'sudo dpkg -i packages-microsoft-prod.deb'
                    sh 'sudo apt update'
                    sh 'sudo apt install -y dotnet-sdk-${DOTNET_VERSION}'
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
                sh 'dotnet build --no-restore'
            }
        }
        
        stage('Run Integration Tests') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
