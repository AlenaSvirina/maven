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
                    sh "mvn -f pre-integration-test"
                },
                'integration-test': {
                    sh "mvn -f integration-test"
                },
                'post-integration-test': {
                    sh "mvn -f post-integration-test"
                }
        )
    }
}
