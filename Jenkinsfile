pipeline {
    agent any

    environment {
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

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('List Files') {
            steps {
                bat 'dir target'
            }
        }

        stage('Rename WAR') {
            steps {
                bat "rename ${env.ORIGINAL_WAR_FILE} ${env.NEW_WAR_FILE}"
            }
        }

        stage('Deploy') {
            steps {
                sshPublisher(publishers: [
                    sshPublisherDesc(
                        configName: REMOTE_SERVER,
                        transfers: [
                            sshTransfer(
                                sourceFiles: WAR_FILE,
                                removePrefix: 'target',
                                remoteDirectory: REMOTE_WEBAPPS_PATH
                            )
                        ]
                    )
                ])
            }
        }
    }
}