pipeline {
    options {    // This is used for log rotation

        buildDiscarder(logRotator(numToKeepStr: '3'))

        disableConcurrentBuilds()

    }

    agent {
        label "windows"
    }
    tools {
        maven 'M3'
        jdk 'JDK 1.8'
    }
    stages {

        stage ('Build') {
            def scmVars = checkout scm
            eraseSnapForMasterBranch scmVars.GIT_BRANCH

            try {
                sh 'mvn clean deploy'
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

}
