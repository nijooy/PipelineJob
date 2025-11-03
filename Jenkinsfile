node {
    stage('Checkout') {
        git 'https://github.com/nijooy/PipelineJob.git'
    }

    stage('Build') {
        try {
            bat 'npm install'
        } catch (e) {
            error "빌드 실패: ${e}"
        }
    }

    stage('Test') {
        def testPassed = bat(script: 'npm test', returnStatus: true)
        if (testPassed != 0) {
            error '테스트 실패!'
        }
    }

    stage('Deploy') {
        if (env.BRANCH_NAME == 'main') {
            bat 'npm start'
        } else {
            echo 'main 브랜치가 아니라서 실행 생략'
        }
    }
}
