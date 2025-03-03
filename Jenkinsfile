pipeline {
    agent any

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }

        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }

        stage('Code Coverage') {
            steps {
                sh './mvnw jacoco:report'
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
