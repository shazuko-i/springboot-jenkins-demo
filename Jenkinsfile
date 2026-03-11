pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = 'C:\\Program Files\\apache-tomcat-10.1.52\\webapps'
        WAR_NAME = 'JenkinsWarFile.war'
    }

    tools {
        // Must match Jenkins Global Tool Configuration
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

        stage('Deploy WAR to Tomcat') {
            steps {
                bat """
                REM Ensure webapps folder exists
                if not exist "%TOMCAT_WEBAPPS%" mkdir "%TOMCAT_WEBAPPS%"

                REM Copy the WAR to Tomcat
                copy target\\%WAR_NAME% "%TOMCAT_WEBAPPS%\\%WAR_NAME%"
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