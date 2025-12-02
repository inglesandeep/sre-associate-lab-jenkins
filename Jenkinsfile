pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build -f containerfile -t snayak225/frontend:jen .'
            }
        }
        stage('Docker Push') {
            agent any
            steps {
                withCredentials([usernamePassword(credentialsId: 'dckr_pat_wXlTOwMQcdRnw2sAVn6P_sEfIXk', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login docker.io -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push snayak225/frontend:jen'
                }
            }
        }
        stage('Docker Run') {
            agent any
            steps {
                sh 'docker run -d -p 12001:12000 snayak225/frontend:jen'
                sh 'docker run -d -p 12002:12000 snayak225/frontend:jen'
                }
            }
        }
    }
