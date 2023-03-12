pipeline {
    agent any
    stages {
        stage('Build Nginx') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y build-essential wget'
                sh 'wget http://nginx.org/download/nginx-1.20.1.tar.gz'
                sh 'tar -xvf nginx-1.20.1.tar.gz'
                dir('nginx-1.20.1') {
                    sh './configure --prefix=/usr/local/nginx --with-http_ssl_module'
                    sh 'make'
                    sh 'make install'
                }
            }
        }
        stage('Copy nginx configuration') {
            steps {
                sh 'mkdir -p /usr/local/nginx/conf'
                sh 'cp /path/to/nginx.conf /usr/local/nginx/conf/'
                // Repeat for any additional configuration files
            }
        }
        stage('Build docker image') {
            steps {
                sh 'docker build -t mynginx .'
            }
        }
        stage('Create Production Container') {
            steps {
                sh 'docker run -d --name mynginxcontainer mynginx'
                sh 'docker cp /path/to/static/html mynginxcontainer:/usr/share/nginx/html'
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
        always {
            sh 'docker rm -f mynginxprodcontainer'
        }
    }
}
