pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Clean the workspace before building
                cleanWs()

                // Run the Gradle assemble task
                sh './gradlew assemble'
            }
        }

        stage('Test') {
            steps {
                // Run the Gradle test task
                sh './gradlew test'
            }
        }
    }

    post {
        always {
            // Archive the build artifacts
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true

            // JUnit result reporting
            junit 'build/test-results/test/*.xml'
        }
        failure {
            // Notify about the failure
            echo 'Build or tests failed. Check the logs for more details.'
        }
    }
}
