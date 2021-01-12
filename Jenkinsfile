pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk11'
    }
    parameters {
        booleanParam(name: "Perform release ?", description: '', defaultValue: false)
    }
    stages {
        stage('Initialize') {
            steps {
                bat '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('Build') {
            steps {
                bat 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                //withMaven(mavenSettingsConfig: 'maven-config', globalMavenSettingsConfig: 'global-config') {
                    //bat "mvn  -s C:/Users/Paul Chaigneau/.m2/settings.xml deploy"
                    bat "mvn  -s E:/Documents/apache-maven-3.6.3-bin/apache-maven-3.6.3/conf/settings.xml deploy"
                //}
            }
        }
        stage('Release') {
            when { expression {  params['Perform release ?']} }
            steps {
                script{
                    pom = readMavenPom file: 'pom.xml'
                }
                withCredentials([usernamePassword(credentialsId: 'chaigneauP', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]){
                    //withMaven(mavenSettingsConfig: 'maven-config', globalMavenSettingsConfig: 'global-config') {
                        bat 'git config --global user.email "chaigneaupaul@gmail.com"'
                        bat 'git config --global user.name "chaigneauP"'
                        bat 'git branch release/'+pom.version.replace("-SNAPSHOT","")
                        bat 'git push origin release/'+pom.version.replace("-SNAPSHOT","")
                        bat 'mvn release:prepare -s -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                        bat 'mvn release:perform -s -B -Dusername=$USERNAME_VAR -Dpassword=$PASSWORD_VAR'
                    //}
                }
            }
        }
        stage('Sonar') {
        //sonar login : admin, psswd : admin, Jenkins-Auth-Token 9dfa1812223d38162b080d5a26f797267ab0859d
            steps {
                withCredentials([usernamePassword(credentialsId: 'chaigneauP', passwordVariable: 'PASSWORD_VAR', usernameVariable: 'USERNAME_VAR')]) {
                    bat "mvn  -s E:/Documents/apache-maven-3.6.3-bin/apache-maven-3.6.3/conf/settings.xml sonar:sonar -Dsonar.login=admin -Dsonar.password=admin"
                }
            }
        }
    }
}