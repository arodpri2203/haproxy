pipeline {
  agent {label 'VPS'}
	
	environment {
		dockerfilePath= "/home/debian/jenkins"
		registry = "arodpri2203/antoniocaso-a:v2"
		registryCredential = 'dockerhub'
	}
	stages {
		stage ('Test') {
			steps {
				sh 'echo executing test'
			}
		}
        stage ('Build Docker') {
			steps {
				script {
					dockerImage = docker.build(registry, "-f ${dockerfilePath}Dockerfile .")
				}
			}
		}
		stage ('Push Docker') {
			steps {
				script {
					docker.withRegistry('', registryCredential){
						dockerImage.push()
					}
				}
			}
		}
		stage ('Run Docker'){
			steps{
				sh 'docker run -d -p 15600:80 ${registry}'
			}
		}
	}
}
