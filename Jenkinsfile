pipeline {
    agent any

    stages {

        stage('Clone GitHub') {
            steps {
                git 'https://github.com:julesy19/Projet-Jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-cicd .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop flask-app || true'
                sh 'docker rm flask-app || true'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name flask-app flask-cicd'
            }
        }
    }
}