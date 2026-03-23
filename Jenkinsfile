pipeline{
    agent any
    tool {
        maven 'maven'
        jdk 'jdk21'
    }
    enviroment {
        TAg = ${env.BUILD_NUMBER}
        image = docker.io/chumaedeogu/app1
    }
    tools {
        maven = tool 'maven'
        jdk = tool 'jdk'
    
    }
     
     stages{
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Docker Build') {
            steps {
                sh "docker build -t ${image}:${TAG} ."
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                    sh "echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin"
                    sh "docker push ${image}:${TAG}"
                }
            }
        }

     }

}