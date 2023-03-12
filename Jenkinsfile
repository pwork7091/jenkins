pipeline {
    agent any
    stages {
        stage('Build in docker') {
            steps {
                script {
                    docker.image('machimachi/docker-node-with-chrome').inside('--privileged -v /tmp:/tmp') {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('deploy') {
            steps {
                sh 'docker rm -f jenkins-test'
                sh 'docker run --rm -v $WORKSPACE/dist/jenkins-test:/usr/share/nginx/html -p 8081:80 --name jenkins-test -d nginx:alpine'
            }
        }
    }
}
