pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven'
    }

    environment {
        IMAGE_NAME = "springboot-tomcat-app"
        CONTAINER_NAME = "springboot-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/syoganandh/spring-boot-maven-example-helloworld.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8082:8080 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
