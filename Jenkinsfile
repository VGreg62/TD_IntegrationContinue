pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				echo 'Build...'
                bat "mvn clean"
				echo 'Validate...'
				bat "mvn validate"
				echo 'Compile...'
				bat "mvn compile"
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true 
            }
        }
        stage('Test') {
            steps {
				echo 'Test...'
                bat 'mvn test'
                junit '/**/*.xml' 
            }
        }
		stage('Package') {
            steps {
				echo 'Package...'
                bat 'mvn package' 
            }
        }
    }
}