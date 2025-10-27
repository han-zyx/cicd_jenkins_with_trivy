pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
	environment {
		SONAR_PROJECT_KEY = 'cicd_with_trivy'
		DOCKER_HUB_REPO = 'hansakatennakoon/cicd_with_trivy'
	}
    stages {
        stage('Github') {
            steps {
                git branch: 'main', credentialsId: 'CICD-jenkins', url: 'https://github.com/han-zyx/cicd_jenkins_with_trivy.git'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'npm test'
                sh 'npm install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'cicd_with_trivy', variable: 'SONAR_TOKEN')]) {
					withSonarQubeEnv('SonarQube') {
						 script {
                            def scannerHome = tool 'SonarQubeScanner'
                            sh """
                                ${scannerHome}/bin/sonar-scanner \
                                -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                                -Dsonar.sources=. \
                                -Dsonar.host.url=http://13.201.90.223:9000 \
                                -Dsonar.login=${SONAR_TOKEN}
                            """
                        }
					}
                }
            }
        }
		stage('Docker Image'){
			steps{
				script{
					docker.build("${DOCKER_HUB_REPO}:latest")
				}
			}
		}
    }
}
