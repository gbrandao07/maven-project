pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Compiling...'
				bat 'mvn clean package'
            }
			post {
				success {
					echo 'Now archiving...'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
        }
		stage('Deploy to Staging') {
			steps {
				build job: 'deploy-to-staging'
			}
		}
		stage('Deploy to Production') {
			steps {
				timeout(time:5, unit:'DAYS') {
					input message: 'Approve PRODUCTION deployment?'
					
					build job: 'deploy-to-prod'
				}
			}
			post {
				success {
					echo 'Code deployed to production.'
				}
				
				failure {
					echo 'Deployment to production failed.'
				}
			}
		}
    }
}