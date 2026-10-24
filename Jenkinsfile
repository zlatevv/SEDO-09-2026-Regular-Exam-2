pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')   // checks GitHub every minute for new commits
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }
    }

    post {
        success { echo 'Build and tests passed.' }
        failure { echo 'Build or tests failed.' }
    }
}