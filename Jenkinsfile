def gv
pipeline {
    agent any
    tools{
        maven 'maven'
        }
    stages {
        stage("build jar") {
            steps {
                script {
                    echo "eco building application.."
                    sh 'mvn_package'
                }
            }
        }

        stage("build image") {
            steps {
                script {
                    echo "building the docker image"
                    withCredentials([usernamePassword(credentialsId:'docker-hub', passwordVariable: 'PASS', userrnameVariable: 'USER')]){
                        sh 'docker build -t muhammedafsal/demo-app:mvn1.1 .'
                        sh "echo $PASS |  docker login -u $USER --password-stdin"
                        sh "docker push muhammedafsal/demo-app:mvn1.1"
                    }
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    //gv.deployApp()
                }
            }
        }
    }   
}
