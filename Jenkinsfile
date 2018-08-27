node {
    stage('Preparation (Checking out)') {
        git branch: 'master', url: 'https://github.com/AlenaSvirina/maven'
    }
    stage('Building code') {
        withMaven {
            sh "mvn package"
        }
    }
    stage("Testing")
    withMaven {
        parallel(
                'pre-integration-test': {
                    sh "mvn pre-integration-test"
                },
                'integration-test': {
                    sh "mvn integration-test"
                },
                'post-integration-test': {
                    sh "mvn post-integration-test"
                }
        )
    }
}
