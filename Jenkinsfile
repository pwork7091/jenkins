pipeline {
    agent any
    stages {
        stage('Build Nginx') {
            steps {
                sh 'docker build -t mynginx .'
            }
        }
        stage('Create Production Container') {
            steps {
                sh 'docker run -d --name mynginxcontainer mynginx'
                sh 'docker cp index.html mynginxcontainer:/usr/share/nginx/html'
                sh 'docker commit mynginxcontainer mynginxprod'
                sh 'docker rm -f mynginxcontainer'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker run -d --name mynginxprodcontainer -p 80:80 mynginxprod'
            }
        }
        stage('Test Container') {
            steps {
                sh 'curl localhost'
            }
        }
    }
    post {
        failure {
            sh 'docker rm -f mynginxprodcontainer'
        }
    }
}
