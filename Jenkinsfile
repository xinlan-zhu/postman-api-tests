pipeline {
    agent any

    // 使用之前在 Jenkins 全局工具中配置的 NodeJS 环境
    tools {
        nodejs 'NodeJS-24'  // 请替换为你在 Jenkins 中配置的 NodeJS 安装名
    }

    stages {
        stage('Run API Tests') {
            steps {
                // 运行 Newman 命令，生成 HTML 报告
                bat 'newman run my-collection.json -r htmlextra --reporter-htmlextra-export newman-report.html'
            }
        }
    }

    post {
        always {
            // 发布测试报告
            publishHTML([
                allowMissing: false,          // 如果报告丢失，构建失败
                alwaysLinkToLastBuild: true,  // 总是链接到最后一次构建
                keepAll: true,                // 保留所有历史报告
                reportDir: '.',               // 报告所在目录，. 表示当前工作空间根目录
                reportFiles: 'newman-report.html', // 报告文件名
                reportName: 'Newman API Test Report' // 报告在 Jenkins 中显示的名称
            ])
        }
    }
}
