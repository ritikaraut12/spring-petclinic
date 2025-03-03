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
        bat './mvnw jacoco:report'  // Run JaCoCo
        script {
            def jacocoDir = 'target/site/jacoco'
            def jacocoReport = "${jacocoDir}/index.html"

            if (fileExists(jacocoReport)) {
                echo "JaCoCo report found!"
                publishHTML(target: [
                    reportDir: jacocoDir,
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Code Coverage'
                ])
            } else {
                error "JaCoCo report not found at ${jacocoReport}"
            }
        }
    }
}
