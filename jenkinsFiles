pipeline {
    agent any

    stages {
        stage('Validate') {
            steps {
                echo 'Validate..'
				sh 'mvn validate'
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile..'
				sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing....'
				sh 'mvn test'
            }
        }
		
		stage('Package'){
			steps{
				echo 'Package....'
				sh 'mvn package'
			}
		}
    }
}