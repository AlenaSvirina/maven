node {
    stage('Preparation (Checking out)') {
        git branch: 'master': 'https://github.com/AlenaSvirina/maven'
    }
    stage('Building code') {
        withMaven {
            sh "mvn ./pom.xml package"
        }
    }
    stage("Testing")
    withMaven {
        parallel(
                'pre-integration-test': {
                    sh "mvn -f ./pom.xml pre-integration-test"
                },
                'integration-test': {
                    sh "mvn -f ./pom.xml integration-test"
                },
                'post-integration-test': {
                    sh "mvn -f ./pom.xml post-integration-test"
                }
        )
    }
}
