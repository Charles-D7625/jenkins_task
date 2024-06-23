pipeline {
    agent any

    environment {
        TOMCAT_USER = 'admin'
        TOMCAT_PASSWORD = 'password'
        TOMCAT_URL = 'http://185.65.200.83:8085/manager/text'
        APP_NAME = 'jenkinstest'
        WAR_FILE = 'target/jenkins_task-0.0.1-SNAPSHOT.war'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Charles-D7625/jenkins_task.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }


        stage('Deploy') {
            steps {
                script {
                    def deployUrl = "${env.TOMCAT_URL}/deploy?path=/${env.APP_NAME}&update=true"
                    bat """
                    curl -v -u ${env.TOMCAT_USER}:${env.TOMCAT_PASSWORD} --upload-file ${env.WAR_FILE} "${deployUrl}"
                    """
                }
            }
        }
    }
}