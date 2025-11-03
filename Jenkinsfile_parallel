pipeline {
    agent none

    stages {
        stage('Parallel Build & Test') {
            parallel {
                stage('Build on Agent1') {
                    agent { label 'agent1' }
                    steps {
                        script {
                            if (isUnix()) {
                                sh '''
                                  echo "Agent1 빌드 수행 중..."
                                  sleep 5
                                  echo "Agent1 빌드 완료!"
                                '''
                            } else {
                                bat '''
                                  @echo off
                                  echo Agent1 빌드 수행 중...
                                  timeout /T 5 /NOBREAK >nul
                                  echo Agent1 빌드 완료!
                                '''
                            }
                        }
                    }
                }

                stage('Test on Agent2') {
                    agent { label 'agent2' }
                    steps {
                        script {
                            if (isUnix()) {
                                sh '''
                                  echo "Agent2 테스트 수행 중..."
                                  sleep 5
                                  echo "Agent2 테스트 완료!"
                                '''
                            } else {
                                bat '''
                                  @echo off
                                  echo Agent2 테스트 수행 중...
                                  timeout /T 5 /NOBREAK >nul
                                  echo Agent2 테스트 완료!
                                '''
                            }
                        }
                    }
                }
            }
        }
    }
}
