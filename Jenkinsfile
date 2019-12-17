pipeline {
    agent any

    stages {
        stage('Package') {
			steps {
				bat 'mvn clean'
				echo 'Package...'
                bat 'mvn package' 
            }
        }
		stage('Analyse') {
			steps {
				echo 'Analyse...'
			}
        }		
    }
	post{
			always{
				archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true 
                junit '/**/*.xml'
			}
		}
}