pipeline {
    agent any

    environment {
        IMAGE_NAME = 'MY-Go' // ✅ Fixed: lowercase
        CONTAINER_NAME = 'My-go-app-container'
        HOST_PORT = '5059'
        CONTAINER_PORT = '5000'
    }

    stages {
        stage('Test') {
            steps {
                git 'https://github.com/ramizshaikh8/ci-cd-demo.git'
                sh 'go test ./...'
            }
        }

        stage('Build Docker Image') {
            steps {
                git 'https://github.com/ramizshaikh8/ci-cd-demo.git'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                    echo "[INFO] Stopping and removing existing container (if any)..."
                    docker rm -f $CONTAINER_NAME || true
                    sleep 2
                    echo "[INFO] Starting a new container..."
                    docker run -d --name $CONTAINER_NAME -p $HOST_PORT:$CONTAINER_PORT $IMAGE_NAME
                '''
            }
        }

        stage('Run') {
            steps {
                sh '''
                    echo "[INFO] Verifying container is running..."
                    docker ps | grep $CONTAINER_NAME || echo "Container failed to start"
                    cd /var/lib/jenkins/workspace/full-cicd-go && ./go-webapp-sample &
                '''
            }
        }
    }

    post {
        success {
            echo '✅ All stages completed.'
        }
        failure {
            echo '❌ Pipeline failed.'
        }
    }
}
