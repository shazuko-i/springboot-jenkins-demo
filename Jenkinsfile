pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = 'C:\\Program Files\\apache-tomcat-10.1.52\\webapps'
        WAR_NAME = 'JenkinsWarFile.war'
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

        stage('Deploy Application') {
            steps {
                bat """
                if not exist "%DEPLOY_DIR%" mkdir "%DEPLOY_DIR%"
                xcopy /E /Y * "%DEPLOY_DIR%"
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