pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\Program Files\\apache-tomcat-10.1.52\\webapps\\php-demo'
    }

    stages {

        stage('Checkout Source') {
            steps {
                checkout scm
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
