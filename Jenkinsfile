node('master') {
    def ngxImage = 'admintuts/nginx:1.19.6-rtmp-geoip2-alpine'
		stage('Git Checkout'){
			git credentialsId: 'git-hub-credentials', url: 'https://github.com/sceptic30/nginx-rtmp-geoip2-alpine'
		}
		stage('Build Docker Image'){
		    sh "docker build . -t ${ngxImage}"
		}
		stage('Push Docker Image'){
			withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'dockerHubPass', usernameVariable: 'dockerHubUsrname')]) {
			    sh "docker login -u ${dockerHubUsrname} -p ${dockerHubPass}"
			    sh "docker push ${ngxImage}"
			}
		}
		stage('Test Nginx Image On Staging Server'){
			def dockerRun = "docker run -p 8080:80 -d --name nginx-test ${ngxImage}"
			sshagent(['remote-server-ssh-credentials']) {
			    sh "ssh -o StrictHostKeyChecking=no root@admintuts.net ${dockerRun}"
			    sh 'ssh -o StrictHostKeyChecking=no root@admintuts.net curl -I http://admintuts.net:8080'
			    sh 'ssh -o StrictHostKeyChecking=no root@admintuts.net docker stop nginx-test'
			    sh 'ssh -o StrictHostKeyChecking=no root@admintuts.net docker rm nginx-test'
            }
		}
}
