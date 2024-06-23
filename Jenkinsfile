pipeline {
    agent any

    environment {
        TOMCAT_CREDS=credentials('ssh-key')
        ORIGINAL_WAR_FILE = "target/jenkins_task-0.0.1-SNAPSHOT.war"
        NEW_WAR_FILE = "target/jenkinstest.war"
        SSH_CREDENTIALS_ID = "github-ssh-key"
        REMOTE_SERVER = "shad@185.65.200.83"
        REMOTE_WEBAPPS_PATH = "/opt/tomcat/webapps"
    }

    stages {

        stage('Checkout') {
            steps {
                sshagent(credentials: [env.SSH_CREDENTIALS_ID]) {
                        sh 'git clone git@github.com:your-username/your-repo.git'
                }
            }
        }
 
        /*stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }*/
 
        stage('Deploy') {
            steps {
                bat """ 
                    scp -i ${env.TOMCAT_CREDS} ${env.ORIGINAL_WAR_FILE} ${env.REMOTE_SERVER}:/tmp/
                """
            }
        }
    }
}