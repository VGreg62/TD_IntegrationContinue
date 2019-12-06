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
				bat 'mvn checkstyle:checkStyle'
            }
        }		
    }
	post{
			always{
				archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true 
                junit '/**/*.xml'
				
				recordIssues enabledForFailure: true, tools: [mavenConsole(), java(), javadoc()]
				recordIssues enabledForFailure: true, tools: checkStyle()
				recordIssues enabledForFailure: true, tools: spotBugs()
				recordIssues enabledForFailure: true, tools: cpd(pattern: '**/target/cpd.xml')
				recordIssues enabledForFailure: true, tools: pmdParser(pattern: '**/target/pmd.xml')
			}
		}
}