currentBuild.displayName = "todo-app-#"+currentBuild.number
pipeline {
    agent any

    stages {
      stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines  -t firestore/todo-be:$BUILD_NUMBER --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t firestore/todo-be:$BUILD_NUMBER --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t firestore/todo-be:$BUILD_NUMBER --target delivery .'
            }
        }
    }
}
