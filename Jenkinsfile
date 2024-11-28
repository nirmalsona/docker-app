pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "my-app-image"  // Replace with your Docker image name
    }
    stages {
        stage('Build and Deploy to EC2') {
            steps {
                sh '''
                sshpass -p 'ubuntu' ssh -o StrictHostKeyChecking=no ubuntu@65.2.175.252 << EOF
                cd ~/docker-app || mkdir ~/docker-app && cd ~/docker-app
                git clone https://github.com/nirmalsona/docker-app.git . || git pull
                docker build -t $DOCKER_IMAGE .
                docker stop $DOCKER_IMAGE || true
                docker rm $DOCKER_IMAGE || true
                docker run -d -p 80:3000 --name $DOCKER_IMAGE $DOCKER_IMAGE
                EOF
                '''
            }
        }
    }
}

