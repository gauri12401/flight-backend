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
                    image 'maven:3.9.9-eclipse-temurin-17'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    mkdir -p .m2/repository
                    mvn -Dmaven.repo.local=$WORKSPACE/.m2/repository clean package -DskipTests
                '''
            }
        }

    }
}