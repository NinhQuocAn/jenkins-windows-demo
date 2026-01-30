pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Dang build .NET project...'
                bat 'dotnet build'
            }
        }
        stage('Run') {
            steps {
                echo 'Dang chay ung dung...'
                bat 'dotnet run'
            }
        }
    }
}