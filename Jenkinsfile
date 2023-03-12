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
                withCredentials([usernamePassword(credentialsId: '6df1b4e3-8fa2-42a7-b986-05448846473a', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'apt-get update'
                    sh 'apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev zlib1g-dev curl'
                    sh 'curl -O http://nginx.org/download/nginx-1.20.2.tar.gz'
                    sh 'tar -zxvf nginx-1.20.2.tar.gz'
                    sh 'cd nginx-1.20.2 && ./configure --prefix=/usr/local/nginx --with-http_ssl_module --with-http_v2_module &&  make &&  make install'
                    sh 'git config --global user.email "pwork7091@gmail.com"'
                    sh 'git config --global user.name "Jenkins"'
                    sh 'git init'
                    sh 'git add .'
                    sh 'git commit -m "Add compiled nginx binary"'
                    sh "git remote add origin https://${USERNAME}:${PASSWORD}@https://github.com/pwork7091/jenkins.git"
                    sh 'git push origin master'
                }
            }
        }
    }
}
