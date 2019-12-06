pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				echo 'Build...'
                bat "mvn clean install"
				echo 'Validate...'
				bat "mvn validate"
				echo 'Compile...'
				bat "mvn compile"                
            }
        }
        stage('Test') {
            steps {
				echo 'Test...'
                bat 'mvn test'
            }
        }
		stage('Package') {
            steps {
				echo 'Package...'
                bat 'mvn package' 
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