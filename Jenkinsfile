pipeline {
    agent {
        any {
            image 'buildpack-deps:latest'
            args '--privileged'
        }
    }
    stages {
        stage('Build nginx') {
            steps {
                sh 'sudo apt-get update'
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
                sh 'docker build -t my-nginx .'
            }
        }
    }
}
