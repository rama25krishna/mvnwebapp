pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/bin/mvn'
    }

    stages {
        stage('Checkout') {
            steps {
                pwd
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                // Example: Copy WAR to Tomcat webapps directory
                sh '''
                    echo Cogdevops_2025 | sudo -S cp target/mvnwebapp.war /opt/tomcat/webapps/
                    systemctl restart tomcat
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
