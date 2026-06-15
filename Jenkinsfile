pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello from Pipeline!'
            }
        }
        stage('World') {
            steps {
                echo 'This is stage 2!'
                sh 'ls -la'
            }
        }
    }
}
