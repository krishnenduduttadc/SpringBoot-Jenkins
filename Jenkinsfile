pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    docker.image('maven:3.9.6-eclipse-temurin-17')
                          .inside {
                              sh 'mvn clean package'
                          }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    docker.image('maven:3.9.6-eclipse-temurin-17')
                          .inside {
                              sh 'mvn test'
                          }
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}