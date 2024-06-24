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
                    sshPublisher(publishers: [sshPublisherDesc(configName: 'server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo mkdir temp', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: 'temp', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'jenkins_task/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
            }
        }
    }
}