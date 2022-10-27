currentBuild.displayName = "todo-app-#"+currentBuild.number
pipeline {
    agent any

    stages {
      stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines  -t build-image:$BUILD_NUMBER --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t test-image:$BUILD_NUMBER --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t firestore/todo-fe:$BUILD_NUMBER --target delivery .'
            }
        }
        stage('Push Artifact') {
            steps{
                withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerPwd')]) {
                sh "docker login -u firestore -p ${dockerPwd}"
        }
                sh "docker push firestore/todo-fe:$BUILD_NUMBER"
            }
        }
    }
}
