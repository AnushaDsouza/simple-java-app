pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t simple-java-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop simple-java-container || true
                docker rm simple-java-container || true

                docker run -d \
                  --name simple-java-container \
                  -p 8081:8080 \
                  simple-java-app
                '''
            }
        }
    }
}