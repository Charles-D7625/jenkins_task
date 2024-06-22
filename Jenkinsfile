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

        stage('Rename WAR') {
            steps {
                script {
                    def warFile = "target/jenkins_task-0.0.1-SNAPSHOT.war"
                    def newWarFile = "target/jenkinstest.war"
                    bat """
                    if exist ${warFile} (
                        rename ${warFile} ${newWarFile}
                    ) else (
                        echo File not found: ${warFile}
                        exit 1
                    )
                    """
                    env.NEW_WAR_FILE = newWarFile
                }
            }
        }

        stage('Deploy') {
            steps {
                powershell '''
                    scp -r "${env.NEW_WAR_FILE} shad@185.65.200.83:/tmp/"
                '''
            }
        }
    }
}