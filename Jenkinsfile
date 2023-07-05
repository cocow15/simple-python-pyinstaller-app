node {
    stage('Build') {
        // Poll SCM every 2 minutes
        properties([
            pipelineTriggers([
                cron('*/2 * * * *')
            ])
        ])

        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            stash(name: 'compiled-results', includes: 'sources/*.py*')
        }
    }

    stage('Test') {
        
    }
}