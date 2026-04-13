pipeline {
    agent any

    tools {
        nodejs 'NodeJS-24'   // 改成你实际配置的名称，比如 'NodeJS-24'
    }

    stages {
        stage('Run API Tests') {
            steps {
                bat 'newman run my-collection.json -r htmlextra --reporter-htmlextra-export newman-report.html'
            }
        }
    }

    post {
        always {
            publishHTML([
                target: [
                    reportDir: '.',
                    reportFiles: 'newman-report.html',
                    reportName: 'Newman Test Report'
                ],
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true
            ])
        }
    }
}
