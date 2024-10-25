pipeline {
	agent { label 'JDK8' }
        stages {
           stage('SourceCode') {
               steps {
                    git branch: 'sprint1_develop', url: 'https://github.com/mailrajeshsre/game-of-life.git'
                  }
           }
           stage('Build the code') {
               steps {
                     mvn package
                  }
           }
           stage('Archiving artifacts & Junit Test Results') {
               steps {
                    junit stdioRetention: '', testResults: '**/surefire-reports/*.xml'
                    archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                 }
           }
      }
}
