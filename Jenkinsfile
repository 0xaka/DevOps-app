pipeline {
    agent any 

    stages {
        stage('Build Assets') {
             agent {
                  docker {
                   image 'maven:3.6.0-jdk-8-alpine'
                   args '-v /root/.m2/repository:/root/.m2/repository'
                   // to use the same node and workdir defined on top-level pipeline for all docker agents
                   reuseNode true
                 }
             }
            steps {
                echo 'Building Assets...'
            }
        }
        stage('Test') {
            agent any
            steps {
                echo 'Testing stuff...'
            }
        }
    }
}
