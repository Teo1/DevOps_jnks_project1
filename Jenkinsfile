pipeline {
    agent any
    tools{
        jdk 'jdk8'
        maven 'maven3'
    }

    stages{
        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }

         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }

         stage("Build"){
            steps{
                sh "mvn clean install"
            }
        }
        stage("Build docker image"){
            steps{
                sh "docker build -t teog1/devops_dh_project1:$env.BUILD_NUMBER ."
            }
        }
        stage("Publish docker image"){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: "docker-credentials", usernameVariable: "DOCKER_REPOSITORY_USER", passwordVariable: "DOCKER_REPOSITORY_PASSWORD")]){
                        sh "docker login -u $DOCKER_REPOSITORY_USER -p $DOCKER_REPOSITORY_PASSWORD"
                        sh "docker push teog1/devops_dh_project1:$env.BUILD_NUMBER"
                    }
                }
            }
        }
    }
}
