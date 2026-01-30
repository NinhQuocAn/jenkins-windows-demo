pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                echo '1. Don dep...'
                bat 'dotnet clean'
            }
        }

        stage('Restore') {
            steps {
                echo '2. Tai thu vien...'
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo '3. Build .NET 8...'
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Run App') {
            steps {
                echo '4. Chay ung dung thu...'
                bat 'dotnet run --configuration Release'
            }
        }

        stage('Archive') {
            steps {
                echo '5. Luu file .exe...'
                archiveArtifacts artifacts: '**/bin/Release/*.exe', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}