pipeline {
    agent any
    tools {
        // Ensure Maven and JDK are installed on the Jenkins node
        maven 'Maven 3.9.6'
        jdk 'OpenJDK 11'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn clean verify'
            }
        }
        stage('SonarQube Scan') {
            environment {
                // SonarQube environment variable defined in Jenkins global config
                SONAR_HOST_URL = credentials('sonar-host-url')
                SONAR_AUTH_TOKEN = credentials('sonar-auth-token')
            }
            steps {
                // Use the SonarScanner Maven plugin
                sh 'mvn sonar:sonar -Dsonar.projectKey=jenkins-sonarqube-sample -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
