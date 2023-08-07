pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-sankar')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh ' docker build -t sankar0812/pythonapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh "docker push sankar0812/pythonapp:$BUILD_NUMBER"
            }
        }
        stage("run docker container"){
            steps{
                sh "docker run -d --name python -p 8090:8090 sankar0812/pythonapp:$BUILD_NUMBER"
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
