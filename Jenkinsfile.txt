pipeline {
    agent any

    environment {
        // Windows에서는 기본 PATH를 자동 인식하므로 별도 설정 필요 없음
        // PATH = "/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
        stage('Start') {
            when {
                branch 'main'
            }
            steps {
                bat 'npm start'
            }
        }
    }
    post {
        success {
            echo 'Pipeline 성공적으로 완료!'
        }
        failure {
            echo 'Pipeline 실패!'
        }
    }
}
