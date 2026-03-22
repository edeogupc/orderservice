pipeline{
    agent any
    tools{
        maven "maven3"
        jdk "jdk21"
    }
    enriornment{
        MYGIT = "chumaedeogu"

    }
    stages{
        stage"clean up"{
            steps{
                cleanWs()
            }
        
        }
        stage "build"{
            steps{
                docker -t myapp:${BUILD_NUMBER} .
                docker tag myapp:$(BUILD_NUMBER) ${MYGIT}/myapp:${BUILD_NUMBER}
                docker push ${MYGIT}/myapp:${BUILD_NUMBER}

            }
        }

    }
}