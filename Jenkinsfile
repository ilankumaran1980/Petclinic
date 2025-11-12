pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Spring Petclinic...'
                // Navigate into spring-petclinic folder to build
                dir('spring-petclinic') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application to Tomcat...'
                sh '''
                sudo systemctl stop tomcat9
                sudo cp spring-petclinic/target/*.jar /var/lib/tomcat9/webapps/petclinic.jar
                sudo systemctl start tomcat9
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
