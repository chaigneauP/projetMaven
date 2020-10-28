pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                mvn compile
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