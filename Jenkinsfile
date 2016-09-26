#!groovy
node {

    stage 'Checkout'
    checkout scm

    withEnv(["MAVEN_OPTS= -XX:+TieredCompilation -XX:TieredStopAtLevel=1"]) {
        def mvnHome = tool 'Maven'
        def mvnOpt = "-T 4 --batch-mode -V -U -e -Dmaven.repo.local=../.m2"
        stage 'Maven Clean'

        sh("${mvnHome}/bin/mvn " + mvnOpt + " clean")

        stage 'Maven package'
        sh("${mvnHome}/bin/mvn " + mvnOpt + " package")
        step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])

    }
}