node('JDK8') {
	stage('SourceCode') {
	//	git branch: 'sprint1_develop', url: 'https://github.com/mailrajeshsre/game-of-life.git'
                checkout scm
       }

	stage('Build the code') {
                // Maven build process
		sh 'mvn clean package'
       }

	stage('Archiving artifacts & Junit Test Results') {
	      junit stdioRetention: '', testResults: '**/surefire-reports/*.xml'
	      archiveArtifacts artifacts: '**/*.war', followSymlinks: false
       }
}
