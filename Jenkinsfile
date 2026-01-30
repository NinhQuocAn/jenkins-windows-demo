pipeline {
    agent any

    stages {
        // --- BƯỚC 1: DỌN DẸP ---
        stage('Clean') {
            steps {
                echo 'Dang don dep cac file build cu...'
                bat 'dotnet clean'
            }
        }

        // --- BƯỚC 2: TẢI THƯ VIỆN (RESTORE) ---
        stage('Restore') {
            steps {
                echo 'Dang tai cac goi NuGet...'
                bat 'dotnet restore'
            }
        }

        // --- BƯỚC 3: BIÊN DỊCH (BUILD) ---
        stage('Build') {
            steps {
                echo 'Dang build project o che do Release...'
                bat 'dotnet build --configuration Release --no-restore'
            }
        }

        // --- BƯỚC 4: KIỂM THỬ TỰ ĐỘNG (TEST) ---
        stage('Unit Test') {
            steps {
                echo 'Chay cac bo test kiem thu chuc nang...'
                bat 'dotnet test --no-build --configuration Release --verbosity normal'
            }
        }

        // --- BƯỚC 5: LƯU TRỮ KẾT QUẢ (ARCHIVE) ---
        stage('Archive Artifacts') {
            steps {
                echo 'Luu lai file .exe de tai ve khi can...'
                // Tu dong tim file exe trong thu muc bin/Release va luu tren Jenkins
                archiveArtifacts artifacts: '**/bin/Release/*.exe', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline hoan tat. Don dep workspace de giai phong bo nho...'
            cleanWs() // Xoa code sau khi build xong
        }
        
        success {
            echo 'THANH CONG: CI Pipeline da chay xong!'
        }
        
        failure {
            echo 'THAT BAI: Co loi xay ra trong qua trinh Build hoac Test.'
        }
    }
}