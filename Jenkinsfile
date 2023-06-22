node {
    stage('Build') {
        // Poll SCM every 2 minutes
        properties([
            pipelineTriggers([
                cron('*/2 * * * *')
            ])
        ])

        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile add2vals.py calc.py'
            stash(name: 'compiled-results', includes: '*.py*')
        }
    }

    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --junit-xml test-reports/results.xml test_calc.py'
        }
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
    }
}