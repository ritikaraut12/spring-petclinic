pipeline {
    agent any

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    stages {
        stage('Build') {
            steps {
                bat './mvnw clean package'  // Change 'sh' to 'bat'
            }
        }

        stage('Test') {
            steps {
                bat './mvnw test'  // Change 'sh' to 'bat'
            }
        }

        stage('Code Coverage') {
            steps {
                bat './mvnw jacoco:report'  // Change 'sh' to 'bat'
                publishHTML(target: [
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Code Coverage'
                ])
            }
        }

        stage('Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}

