pipeline {
    agent any
    
    options {
        skipDefaultCheckout()
    }
        
    stages {
        
        stage('SCM') {
           steps {
            checkout scm
           }
        }
        
        stage('Compile') {
            steps {
                sh ' mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
