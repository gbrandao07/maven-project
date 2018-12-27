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
    }
}