pipeline {
    agent any

    tools {
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
            steps {

                withSonarQubeEnv('sonar-host-url') {

                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=jenkins-sonarqube-sample
                    '''
                }
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
