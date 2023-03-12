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
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev'
                sh 'wget http://nginx.org/download/nginx-1.20.2.tar.gz'
                sh 'tar -zxvf nginx-1.20.2.tar.gz'
                sh 'cd nginx-1.20.2 && sudo ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module && sudo make && sudo make install'
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
