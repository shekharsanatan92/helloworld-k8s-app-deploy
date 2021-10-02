pipeline {
    agent any
    stages {
		stage('Build and Push Image stage') {

		when {
			branch 'master'
		}
		steps {
			script {
			dockerImageApi = docker.build("ss-docker-repo")
			docker.withRegistry('https://746103488160.dkr.ecr.us-east-1.amazonaws.com/ss-docker-repo',"ecr:us-east-1:ci-user") {
				dockerImageApi.push("${env.BUILD_NUMBER}")
				dockerImageApi.push("latest")
			}
			}
		}
		}


        stage('Deploy stage') {
		when {
			branch 'master'
		}
            steps {
				deleteDir()
				checkout scm
				script {
					sh " chmod 755 ./helm-deploy.sh"
					sh " ls -la"
					sh " ./helm-deploy.sh"
				}
            }
	}

    }
}
