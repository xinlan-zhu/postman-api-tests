pipeline {
    agent any

    tools {
        nodejs 'Node25'
    }

    stages {
        stage('Checkout') {
            steps {
                // 当使用 Pipeline script from SCM 时，仓库已经自动拉取到工作空间，这里不需要再写 checkout scm
                // 但如果你想显式拉取，可以保留，不过通常不需要
                script {
                    def workspace = pwd()
                    echo "Running in workspace: ${workspace}"
                }
            }
        }

        stage('Run API Tests') {
            steps {
        // 在Windows上使用bat步骤
        bat 'newman run my-collection.json -r htmlextra --reporter-htmlextra-export newman-report.html'
    }
        }
    }

    post {
        always {
            publishHTML([
                reportDir: '.',
                reportFiles: 'newman-report.html',
                reportName: 'Postman API Test Report'
            ])
        }
    }
}
