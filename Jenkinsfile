pipeline {
	agent any
		stages {
			stage ('Checkout') {
				steps {
					git '/home/GitHub/Vulnerable-Web-Application'
				}
			}
			stage('Code Quality Check via SonarQube') {
				steps {
					script {
						def scannerHome = tool 'SonarQube';
						withSonarQubeEnv('SonarQube') {
							sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=."
						}
					}
				}
			}
		}
		post {
			always {
				recordIssues enabledForFailure: true, tool: sonarQube()
			}
		}
}

