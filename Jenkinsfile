pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                echo '1. Dang don dep solution...'
                // Build file solution de lam viec voi nhieu project
                bat 'dotnet clean JenkinsDemo.sln'
            }
        }

        stage('Restore') {
            steps {
                echo '2. Dang tai thu vien cho ca solution...'
                bat 'dotnet restore JenkinsDemo.sln'
            }
        }

        stage('Build') {
            steps {
                echo '3. Dang build solution .NET 8...'
                // Build file solution, no se xu ly duoc 2 project rieng biet
                bat 'dotnet build JenkinsDemo.sln --configuration Release'
            }
        }

        stage('Unit Test') {
            steps {
                echo '4. Dang chay test...'
                // Test solution
                bat 'dotnet test JenkinsDemo.sln --no-build --configuration Release --verbosity normal'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo '5. Luu tru file .exe...'
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