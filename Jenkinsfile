pipeline {
    agent { label 'JDK8' }

    environment {
        BUILD_USER = "${env.BUILD_USER_ID ?: 'Unknown'}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'sprint1_develop', url: 'https://github.com/Roop-14/Dev-Ops-Project.git'
            }
        }

        stage('Build using Java 8') {
            steps {
                withEnv([
                    "JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64",
                    "PATH=/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"
                ]) {
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

    post {
        success {
            emailext(
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                to: "roopammondal14@gmail.com",
                body: """
                    <h3 style='color:green;'>Build SUCCESS ✔</h3>
                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Triggered by:</b> ${BUILD_USER}</p>
                    <p><a href="${env.BUILD_URL}console">Click here for Console Output</a></p>
                """,
                mimeType: 'text/html'
            )
        }

        failure {
            emailext(
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                to: "roopammondal14@gmail.com",
                body: """
                    <h3 style='color:red;'>Build FAILED ✘</h3>
                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Triggered by:</b> ${BUILD_USER}</p>
                    <p><a href="${env.BUILD_URL}console">Click here for Console Output</a></p>
                """,
                mimeType: 'text/html'
            )
        }
    }
}

