pipeline {
    agent any

    stages {
        stage('Build nginx') {
            steps {
               
                sh 'docker build -t nginx-build -f Dockerfile.build .'
            }
        }
        stage('Create production container') {
            steps {
                sh 'docker build -t nginx-production -f Dockerfile.production .'
            }
        }
        stage('Run container') {
            steps {
                sh 'docker run -d --name nginx -p 80:80 nginx-production'
            }
        }
    }
}
