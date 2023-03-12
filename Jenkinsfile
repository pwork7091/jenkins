pipeline {
    agent {
        docker {
            image 'centos:centos8'
            args '-p 80:80'
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
                sh 'dnf -y update'
                sh 'dnf -y install nginx'
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
