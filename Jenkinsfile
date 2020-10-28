pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "mvn -B compile"
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