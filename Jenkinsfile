pipeline {
    agent {
        any {
            image 'ubuntu:latest'
             user 'root'

        }
    }
    stages {
        stage('Build nginx') {
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
                sh 'sudo mkdir -p /usr/local/nginx/conf'
                sh 'sudo cp /path/to/nginx.conf /usr/local/nginx/conf/'
                // Repeat for any additional configuration files
            }
        }
        stage('Build docker image') {
            steps {
                sh 'sudo docker build -t my-nginx .'
            }
        }
        stage('Create production container') {
            steps {
                sh 'sudo docker run -d --name my-nginx-container my-nginx'
                sh 'sudo docker cp /path/to/static/html my-nginx-container:/usr/share/nginx/html'
                sh 'sudo docker commit my-nginx-container my-nginx-prod'
                sh 'sudo docker rm -f my-nginx-container'
            }
        }
    }
}
