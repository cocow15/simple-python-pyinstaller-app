node {
    stage('Build') {
        // Poll SCM every 2 minutes
        properties([
            pipelineTriggers([
                [$class: 'PollSCM', cron: '*/2 * * * *']
            ])
        ])

        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            stash(name: 'compiled-results', includes: 'sources/*.py*')
        }
    }

    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
        }
        post {
            always {
                junit 'test-reports/results.xml'
            }
        }
    }
}

