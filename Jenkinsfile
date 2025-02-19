pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')  // Runs every 10 minutes on Mondays
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Run the Maven build (you can modify this command based on your setup)
                    sh './mvnw clean install'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    // Run the Jacoco code coverage analysis
                    sh './mvnw clean test jacoco:report'
                }
            }
        }

        stage('Archive Coverage Report') {
            steps {
                // Archive Jacoco coverage reports (located in target/site/jacoco)
                archiveArtifacts artifacts: 'target/site/jacoco/**/*', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Clean up any resources or notify on failure
        }
    }
}
