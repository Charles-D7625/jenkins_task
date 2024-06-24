pipeline {
    agent any

    environment {
        TOMCAT_CREDS=credentials('tomcat-ssh-key')
        ORIGINAL_WAR_FILE = "target/jenkins_task-0.0.1-SNAPSHOT.war"
        NEW_WAR_FILE = "target/jenkinstest.war"
        SSH_CREDENTIALS_ID = "github-ssh-key"
        REMOTE_SERVER = "shad@185.65.200.83"
        REMOTE_WEBAPPS_PATH = "/opt/tomcat/webapps"
    }

    stages {

        /*stage('Checkout') {
            steps {
                git url: 'https://github.com/Charles-D7625/jenkins_task.git', branch: 'master'
            }
        }
 
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }*/
  
        stage('Deploy') {
            steps {
                script  {
                    withCredentials([sshUserPrivateKey(credentialsId: 'tomcat-ssh-key', keyFileVariable: 'KEYFILE', passphraseVariable: '', usernameVariable: 'shad')]) {
                        // Копирование WAR файла на удаленный сервер
                        // Перезапуск Tomcat на удаленном сервере
                        bat """
                            @echo off
                            echo Connect Tomcat on remote server
                            ssh -i %KEYFILE% -o StrictHostKeyChecking=no shad@185.65.200.83 "sudo ls"
                        """
                    } 
                }
            }
        }
    }
}