pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('amitsharma321')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git ' https://github.com/johnpapa/node-hello'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t amit/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push amit/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
stage('Deploying Node.js container to Kubernetes') {
steps {
script {
kubernetesDeploy(configs: "statefulset.yaml", "service.yaml")

}      
}
} 
}
