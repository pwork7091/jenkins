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
                sh 'apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev zlib1g-dev curl'
                sh 'curl -O http://nginx.org/download/nginx-1.20.2.tar.gz'
                sh 'tar -zxvf nginx-1.20.2.tar.gz'
                sh 'cd nginx-1.20.2 && ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module && make &&  make install'
            }
        }
    }
}
