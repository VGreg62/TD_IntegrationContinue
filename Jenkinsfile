pipeline {
    agent any

    stages {
        stage('Package') {
			steps {
			    /*bat 'mvn checkstyle:checkstyle'*/
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
            nexusPublisher nexusInstanceId: 'nexus_localhost', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'word-count', groupId: 'cicd.learn.tp1', packaging: 'jar', version: '1.1']]], tagName: '1.1'

		    /*recordIssues enabledForFailure: true, tools: [mavenConsole(), java()]
			recordIssues enabledForFailure: true, tools: checkStyle()
			recordIssues enabledForFailure: true, tools: spotBugs()
			recordIssues enabledForFailure: true, tools: cpd(pattern: '**/target/cpd.xml')
			recordIssues enabledForFailure: true, tools: pmdParser(pattern: '**/target/pmd.xml')*/
		}
	}
}