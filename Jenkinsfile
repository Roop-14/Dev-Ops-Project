pipeline {
    agent { label 'JDK8' }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'sprint1_develop', url: 'https://github.com/Roop-14/Dev-Ops-Project.git'
            }
        }
        stage('Build using Java 8') {
            steps {
                withEnv(["JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64", "PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"]) {
                    sh 'java -version'
                    sh 'mvn clean package'
                }
            }
        }
        stage('Archive & Test Results') {
            steps {
                junit '**/surefire-reports/*.xml'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
    }
}

