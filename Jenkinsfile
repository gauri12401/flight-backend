pipeline {

    agent any

    environment {
        DOCKER_USER = "gauri128"
        DOCKER_REPO = "flight-backend"
        IMAGE_NAME  = "flight-backend"
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
                    docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .
                '''
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
                    '''
                }
            }
        }

        stage('Docker Tag') {
            steps {
                sh '''
                    docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${DOCKER_USER}/${DOCKER_REPO}:${BUILD_NUMBER}
                '''
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                    docker push ${DOCKER_USER}/${DOCKER_REPO}:${BUILD_NUMBER}
                '''
            }
        }

        stage('Remove Local Images') {
            steps {
                sh '''
                    docker rmi -f ${IMAGE_NAME}:${BUILD_NUMBER}
                    docker rmi -f ${DOCKER_USER}/${DOCKER_REPO}:${BUILD_NUMBER}
                '''
            }
        }

    }

}