pipeline {
	stages {
		stage('Github'){
			steps{
				git branch: 'main', credentialsId: 'CICD-jenkins', url: 'https://github.com/han-zyx/cicd_jenkins_with_trivy.git'
			}
		}
	}
}