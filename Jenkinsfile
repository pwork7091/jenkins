pipeline {
    agent {
        any {
            image 'ubuntu:latest'
            label 'docker'
            args '--user=root'
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
                sh 'apt-get update && apt-get install -y build-essential wget zlib1g-dev libpcre3-dev libssl-dev'
                sh 'wget http://nginx.org/download/nginx-1.20.1.tar.gz'
                sh 'tar -xvzf nginx-1.20.1.tar.gz'
                sh 'cd nginx-1.20.1 && ./configure --with-http_ssl_module && make && make install'
            }
        }
    }
}
