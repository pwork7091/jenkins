pipeline {
    agent {
        docker {
            image 'ubuntu:latest'
            args '-u root:root'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'apt-get update'
                sh 'apt-get -y install nginx'
                sh 'mkdir -p /etc/nginx/conf.d'
                sh 'cp conf/jenkins.conf /etc/nginx/conf.d/jenkins.conf'
                sh 'cp conf/nginx.conf /etc/nginx/nginx.conf'
            }
        }
    }
    post {
        always {
            sh 'nginx -t' // Test the configuration
            sh 'nginx' // Start NGINX
        }
    }
}
