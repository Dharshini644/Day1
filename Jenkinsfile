pipeline {
    agent {
        docker { image 'docker:24.0.5' args '-v /var/run/docker.sock:/var/run/docker.sock' }
    }
    tools{
        maven 'Maven'
        jdk 'jdk'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dharshini644/Day1.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sample-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run --rm sample-app'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}