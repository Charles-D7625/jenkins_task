pipeline {
    agent any

    environment {
        ORIGINAL_WAR_FILE = 'target/jenkins_task-0.0.1-SNAPSHOT.war'
        NEW_WAR_FILE = 'target/enkinstesk.war'
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

    post {
        failure {
            mail to: 'your-email@example.com',
                 subject: "Build failed in Jenkins: ${currentBuild.fullDisplayName}",
                 body: "Something is wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}.\nCheck the logs at ${env.BUILD_URL}"
        }
    }
}