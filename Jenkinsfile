pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'vishnu063/streamlit-app'
        DOCKER_TAG = "${env.BUILD_ID}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Vishnu063/Project123.git', branch: 'master'
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .'
                sh 'docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest'
            }
        }
        
        stage('Deploy') {
            steps {
                sh '''
                    docker stop streamlit-app || true
                    docker rm streamlit-app || true
                    docker run -d -p 8501:8501 --name streamlit-app ${DOCKER_IMAGE}:latest
                '''
            }
        }
    }
}
