currentBuild.displayName = "todo-app-#"+currentBuild.number
pipeline {
    agent any

    stages {
      stage('Build stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines  -t firestore/todo-be:latest --target builder .'
            }
        }
        stage('Test stage') {
            steps {
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t firestore/todo-be:latest --target test .'
            }
        }
        stage('Delivery stage') {
            steps {
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t firestore/todo-be:latest --target delivery .'
            }
        }
    }
}
