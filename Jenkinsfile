pipeline{
    angent any
    tools{
        maven 'mvn'
        jdk 'jdk21'
    }
    environment {
        TAG = "${BUILD_NUMBER}"
        imageName = "chumaedeogu/app"

    }
     stages{
        stage("build stage"){
            steps{
                sh 'docker build -t $imageName:$TAG - t $imageName:latest .'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub1', passwordVariable: 'DOCKER+PWD', usernameVariable: 'DOCKER_USER')]) {
                    sh 'echo $DOCKER_PWD | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $imageName:$TAG'
                    sh 'docker push $imageName:latest'
                }
            }
    // some block
}

            }
        }


     
