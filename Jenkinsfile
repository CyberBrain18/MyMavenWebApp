pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-token', 
                    url: 'https://github.com/cyberBrain18/MyMavenWebApp.git', 
                    branch: 'master'
            }
        }

        stage('Build & Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'sudo cp target/MymavenWebApp-1.0-SNAPSHOT.war /opt/tomcat/webapps/MymavenWebApp01.war'
            }
        }
    }

    post {
        success {
            echo "Successfully deployed MymavenWebApp01 to Tomcat on port 9090."
        }
        failure {
            echo "Pipeline failed. Check Jenkins tool names or sudo permissions."
        }
    }
}
