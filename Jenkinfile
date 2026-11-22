pipeline {
    agent any 
    environment {
    PATH = "/Users/Owner/.docker/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    }

    stages {
        
        stage('Checkout Code') {
            steps {
                echo 'Code successfully pulled from GitHub!'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building the todo-app Docker image...'
                sh 'docker build . -t todo-pipeline-app'
            }
        }
        
        stage('Cleanup Old Container') {
            steps {
                echo 'Removing old container if it exists...'
                sh 'docker rm -f todo-pipeline-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                echo 'Starting the new container on port 3000...'
                sh 'docker run -p 3000:3000 -d --name todo-pipeline-container todo-pipeline-app'
            }
        }
    }

    // What to do after the pipeline finishes
    post {
        always {
            echo 'Pipeline execution finished!'
        }
    }
}
