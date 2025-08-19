pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-django-app"
        CONTAINER_NAME = "django-container"
        PORT = "8000"   // Change if your app uses another port
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Gitikakau/DjangoAppWithDevOps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                    if [ $(docker ps -q -f name=$CONTAINER_NAME) ]; then
                        docker stop $CONTAINER_NAME
                        docker rm $CONTAINER_NAME
                    fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name $CONTAINER_NAME -p $PORT:$PORT $IMAGE_NAME'
            }
        }
    }

    post {
        always {
            echo "Pipeline execution finished!"
        }
    }
}

