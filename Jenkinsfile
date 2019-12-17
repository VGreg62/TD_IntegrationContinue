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
        stage('Publish'){
            steps{
                echo 'Publish...'
                bat 'mvn deploy'
                nexusPublisher nexusInstanceId: 'nexus_localhost', nexusRepositoryId: 'maven-snapshots', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/target/word-count-1.1-SNAPSHOT.jar']], mavenCoordinate: [artifactId: 'word-count', groupId: 'cicd.learn.tp1', packaging: 'jar', version: '1.1-SNAPSHOT']]], tagName: '1.1'
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