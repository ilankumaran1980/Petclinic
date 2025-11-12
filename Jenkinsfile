pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match Maven name in Jenkins
        jdk 'JDK11'      // Must match JDK name in Jenkins
    }

    environment {
        PATH = "/opt/maven/bin:${env.PATH}"  // Ensure mvn command works
        TOMCAT_HOME = "/usr/share/tomcat9"
        APP_NAME = "petclinic"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ilankumaran1980/Petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp target/*.war $TOMCAT_HOME/webapps/$APP_NAME.war
                sudo systemctl restart tomcat9
                '''
            }
        }
    }

    post {
        success { echo 'Deployment completed successfully!' }
        failure { echo 'Deployment failed. Check logs!' }
    }
}
