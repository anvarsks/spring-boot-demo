pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anvarsks/spring-boot-demo.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Stop old container') {
            steps {
                sh 'docker rm -f myapp || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d --name myapp -p 8081:8081 myapp:latest'
            }
        }
    }
}
