pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "mvn install"
                sh "mvn compile"
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