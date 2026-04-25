pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/vvce23ise0101-eng/docker-demo1.git'
            }
        }

        stage('Build Image') {
            steps {
                bat 'docker build -t myapp .'
            }
        }

        stage('Tag Image') {
            steps {
                bat 'docker tag myapp srsuhtir/myapp:v1'
            }
        }

        stage('Login DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {
                    bat 'echo $PASS | docker login -u %$USER% --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                bat 'docker push srsuhtir/myapp:v1'
            }
        }
    }
}