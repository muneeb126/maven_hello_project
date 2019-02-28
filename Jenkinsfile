#!groovy
node ('M3') {
  stage ('Build') {
    def scmVars = checkout scm
    eraseSnapForMasterBranch scmVars.GIT_BRANCH

    try {
      sh '${M3}/bin/mvn clean deploy'
    } finally {
      junit 'target/surefire-reports/*.xml'
    }
  }
}

// TODO - extract into shared lib
def eraseSnapForMasterBranch(branchName) {
  if (branchName == 'master') {
    def pom = readMavenPom file: 'pom.xml'
    if (pom.version.contains('-SNAPSHOT')) {
      pom.version = pom.version.substring(0, pom.version.indexOf('-SNAPSHOT'))
    }
    writeMavenPom pom
  }
}

