pipeline {
    agent any

    tools {
        maven 'mvn'
        jdk 'jdk21'
    }

    environment {
        TAG = "${BUILD_NUMBER}"
        imageName = "chumaedeogu/app"
    }

    stages {

        stage("Build Image") {
            steps {
                sh 'docker build -t $imageName:$TAG -t $imageName:latest .'
            }
        }

        stage("Push Image") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub1',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PWD'
                )]) {

                    sh 'echo $DOCKER_PWD | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $imageName:$TAG'
                    sh 'docker push $imageName:latest'
                }
            }
        }
    }
}
     
