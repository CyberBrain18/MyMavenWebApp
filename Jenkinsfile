pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Build & Deploy') {
            steps {
                git url: 'https://github.com/cyberBrain18/MyMavenWebApp.git', branch: 'master'
                sh 'mvn clean package'
                sh 'cp target/MymavenWebApp-1.0-SNAPSHOT.war /opt/tomcat/webapps/MymavenWebApp01.war'
            }
        }
    }
}
