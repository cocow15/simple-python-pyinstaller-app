node {
    stage('Build') {
        // Poll SCM every 2 minutes
        properties([
            pipelineTriggers([
                cron('*/2 * * * *')
            ])
        ])
    }
}