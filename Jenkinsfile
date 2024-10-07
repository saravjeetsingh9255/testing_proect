pipeline{
    agent any
    stages{
        stage("Code"){
            steps{
                git url:"https://github.com/saravjeetsingh9255/testing_proect.git",branch: "master"
            }
        }
        stage("Build"){
            steps{
                echo "building"
                sh "docker build -t react-app-test-deploy ."
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "push"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubpass",usernameVariable:"dockerhubuser")]){
                    sh "docker tag react-app-test-deploy ${env.dockerhubuser}/reactapp-test-deploy:v1 "
                    sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                    sh "docker push ${env.dockerhubuser}/reactapp-test-deploy:v1"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
