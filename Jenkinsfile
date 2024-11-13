pipeline {
    agent any
     stages {
        stage('BRAKEMAN') {
            steps {
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data --severity-level all -f json -o /data/report1.json'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data  --confidence-level all -f json -o /data/report2.json'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f json -o /data/report3.json'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f html -o /data/report.html'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f csv -o /data/report.csv'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f xml -o /data/report.xml'
                sh ' docker run -v $(pwd):/data -v ./config.yml:/data/config.yml ghcr.io/pycqa/bandit/bandit:latest -r /data -c /data/config.yml -o /data/report4.json'
            }
        post {
         always {
                 recordIssues tools: [
                      bandit(id: 'bandit1', pattern: 'report1.json'),
                      bandit(id: 'bandit2', pattern: 'report2.json'),
                      bandit(id: 'bandit3', pattern: 'report3.json'),
                      bandit(id: 'bandit4', pattern: 'report4.json'),
                      bandit(id: 'bandit5', pattern: 'report.xml')
                    ]
                 publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: '/var/lib/jenkins/workspace/BANDIT',
                    reportFiles: 'report.html',
                    reportName: 'BANDIT'
                    ])
                }
            }
        }
    }
}
