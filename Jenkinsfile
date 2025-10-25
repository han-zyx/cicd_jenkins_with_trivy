pipeline {
	agent any
	tools {
		nodejs 'NodeJS'
	}
	stages {
		stage('Github'){
			steps{
				git branch: 'main', credentialsId: 'CICD-jenkins', url: 'https://github.com/han-zyx/cicd_jenkins_with_trivy.git'
			}
		}
		stage('Unit Test'){
			steps{
				sh 'sudo apt-get update && sudo apt-get install -y libatomic1'
				sh 'npm test'
				sh 'npm install'
			}
		}
	}
}