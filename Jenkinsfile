pipeline {
    agent 'any'
    stages {
        stage ('Build') {
            agent {
                  docker {
                   image 'maven:3.6.0-jdk-8-alpine'
                   args '-v /root/.m2/repository:/root/.m2/repository'
                   // to use the same node and workdir defined on top-level pipeline for all docker agents
                   reuseNode true
                  }
            steps {
                sh '${M2_HOME}/bin/mvn --batch-mode -V -U -e clean verify -Dsurefire.useFile=false -Dmaven.test.failure.ignore'
            }
        }

        stage ('Analysis') {
             agent {
              docker {
               image 'maven:3.6.0-jdk-8-alpine'
               args '-v /root/.m2/repository:/root/.m2/repository'
               reuseNode true
              }
             }
            steps {
                sh '${M2_HOME}/bin/mvn --batch-mode -V -U -e checkstyle:checkstyle pmd:pmd pmd:cpd findbugs:findbugs spotbugs:spotbugs'
            }
        }
    }
    post {
        always {
            junit testResults: '**/target/surefire-reports/TEST-*.xml'

            recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javaDoc()]
            recordIssues enabledForFailure: true, tool: checkStyle()
            recordIssues enabledForFailure: true, tool: spotBugs()
            recordIssues enabledForFailure: true, tool: cpd(pattern: '**/target/cpd.xml')
            recordIssues enabledForFailure: true, tool: pmdParser(pattern: '**/target/pmd.xml')
        }
    }
}
