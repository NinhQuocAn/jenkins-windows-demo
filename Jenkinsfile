pipeline {
    agent any

    stages {
        stage('Clean') {
            steps {
                echo '1. Dang don dep project...'
                bat 'dotnet clean'
            }
        }

        stage('Restore') {
            steps {
                echo '2. Dang tai thu vien (NuGet)...'
                // Bỏ tham số --no-restore để buộc tải lại sạch sẽ
                bat 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo '3. Dang build .NET 8...'
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Unit Test') {
            steps {
                echo '4. Dang chay bo kiem thu...'
                bat 'dotnet test --no-build --configuration Release --verbosity normal'
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
            echo 'Pipeline hoan tat.'
            cleanWs()
        }
    }
}