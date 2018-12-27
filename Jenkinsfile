pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Compiling...'
				sh 'mvn clean package'
            }
			post {
				echo 'Now archiving...'
				archiveArtifacts artifacts: '**/target/*.war'
			}
        }
    }
}