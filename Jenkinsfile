pipeline {

    agent any

    environment {
        DOCKER_USER = "gauri128"
        DOCKER_REPO = "flight-backend"
    }

    stages {

        stage('Git Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/gauri12401/flight-backend.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t ${DOCKER_USER}/${DOCKER_REPO}:${BUILD_NUMBER} .
                '''
            }
        }

    }

}