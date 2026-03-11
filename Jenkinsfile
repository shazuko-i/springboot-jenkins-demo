pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = 'C:\\Program Files\\apache-tomcat-10.1.52\\webapps'
        WAR_NAME = 'springboot-jenkins-demo.war'
    }

    tools {
            // Name must match what you configured in Jenkins → Global Tool Configuration
            maven 'Maven 3'
            jdk 'JDK 17'
        }

    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat """
                copy /Y target\\%WAR_NAME% "%TOMCAT_WEBAPPS%\\%WAR_NAME%"
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}