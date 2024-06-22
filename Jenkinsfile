pipeline {
    agent any

    environment {
        TOMCAT_CREDS=credentials('id-rsa')
        ORIGINAL_WAR_FILE = 'target/jenkins_task-0.0.1-SNAPSHOT.war'
        NEW_WAR_FILE = 'target/jenkinstest.war'
        SSH_CREDENTIALS_ID = 'github-ssh-key'
        REMOTE_SERVER = 'shad@185.65.200.83'
        REMOTE_WEBAPPS_PATH = '/opt/tomcat/webapps'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Charles-D7625/jenkins_task', branch: 'master'
            }
        }

        /*stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }*/

        stage('Deploy') {
            steps {
                sh '''
                    scp -i $TOMCAT_CREDS "C:/ProgramData/Jenkins/.jenkins/workspace/tomcat-pipeline/target/jenkins_task-0.0.1-SNAPSHOT.war" shad@185.65.200.83:/tmp/
                '''
            }
        }
    }
}