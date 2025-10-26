pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
	environment {
		SONAR_PROJECT_KEY = 'cicd_with_trivy'
		SONAR_SCANNER_HOME = 'SonarQubeScanner'
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
						sh """
						${SONAR_SCANNER_HOME}/bin/sonar-scanner \
						-Dsonar.projectKey=${SONAR_PROJECT_KEY} \
						-Dsonar.sources=. \
						-Dsonar.host.url=http://13.233.119.82:9000 \
						-Dsonar.login=${SONAR_TOKEN}
						"""
					}
                }
            }
        }
    }
}
