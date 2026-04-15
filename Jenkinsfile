pipeline {
    agent any

    tools {
        // These names must match what you set in 'Global Tool Configuration'
        maven 'Maven'
        jdk 'JDK'
    }

    stages {
        stage('Cleanup Workspace') {
            steps {
                // Ensures a clean build environment [cite: 76]
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                // Pulls the code from your specific GitHub repository
                git credentialsId: 'github-token', 
                    url: 'https://github.com/cyberBrain18/MyMavenWebApp.git', 
                    branch: 'master'
            }
        }

        stage('Build & Package') {
            steps {
                // Compiles the code and creates the WAR file [cite: 76, 89]
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Copies the generated WAR file to the Tomcat webapps directory 
                // We rename it to MymavenWebApp01.war to match your required URL path [cite: 58]
                sh 'sudo cp target/MymavenWebApp-1.0-SNAPSHOT.war /opt/tomcat/webapps/MymavenWebApp01.war'
                
                echo 'Deployment complete. Access at http://localhost:9090/MymavenWebApp01/' [cite: 94, 95]
            }
        }
    }

    post {
        success {
            echo "Successfully deployed MymavenWebApp01 to Tomcat on port 9090." [cite: 95, 96]
        }
        failure {
            echo "Pipeline failed. Verify Jenkins has sudo permission to copy to /opt/tomcat/webapps." [cite: 93]
        }
    }
}
