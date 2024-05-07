pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_id')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ylmt/flaskapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker tag ylmt/flaskapp:$BUILD_NUMBER maha2620/sample:flaskapp'
                sh 'docker push maha2620/sample:flaskapp'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
