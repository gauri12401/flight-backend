pipeline {

    agent any

    stages {

        stage('Git Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/gauri12401/flight-backend.git'
            }
        }

        stage('Maven Build') {
            agent {
                docker {
                    image 'maven:3.9.9-eclipse-temurin-21'
                    reuseNode true
                }
            }

            environment {
                HOME = "${WORKSPACE}"
            }

            steps {
                sh '''
                    mkdir -p $HOME/.m2/repository
                    mvn clean package
                '''
            }
        }

    }

}