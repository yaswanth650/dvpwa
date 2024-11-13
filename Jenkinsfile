pipeline {
    agent any
     stages {
        stage('BRAKEMAN') {
            steps {
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data --severity-level all -f json -o /data/report1.json || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data  --confidence-level all -f json -o /data/report2.json || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f json -o /data/report3.json || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f html -o /data/report.html || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f csv -o /data/report.csv || true'
                sh 'docker run --rm -v $(pwd):/data ghcr.io/pycqa/bandit/bandit -r /data -f xml -o /data/report.xml || true'
                sh ' docker run -v $(pwd):/data -v ./config.yml:/data/config.yml ghcr.io/pycqa/bandit/bandit:latest -r /data -c /data/config.yml -o /data/report4.json || true'
            }
        }
    }
}
