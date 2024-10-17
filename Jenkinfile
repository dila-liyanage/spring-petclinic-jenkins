pipeline {
    agent any 

    triggers {
        cron('H */10 * * 1') // Triggers every 10 minutes on Mondays
    }

    stages {
        stage('Build and Test') {
            steps {
                script {
                    // Ensure you have Maven installed in your Jenkins instance
                    // Run Maven to build the project and generate the Jacoco report
                    sh 'mvn clean verify'
                }
            }
        }

        stage('Jacoco Code Coverage') {
            steps {
                script {
                    // Assuming the Jacoco report is generated in the target/site/jacoco
                    // Archive the Jacoco report
                    sh 'mvn jacoco:report'
                    // You can add a step to publish the Jacoco report in Jenkins
                    publishHTML(target: [
                        reportDir: 'target/site/jacoco',
                        reportFiles: 'index.html',
                        reportName: 'Jacoco Coverage Report',
                        alwaysLinkToLastBuild: true
                    ])
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace after the build
            cleanWs()
        }
    }
}
