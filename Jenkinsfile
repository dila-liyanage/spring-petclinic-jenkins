pipeline {
    agent any 

    triggers {
        cron('H */10 * * 1') // Triggers every 10 minutes on Mondays
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'main', 
                        url: 'https://github.com/dila-liyanage/spring-petclinic-jenkins.git', 
                        credentialsId: '<your-credential-id>' // Replace with your credentials ID
                }
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    // Ensure you have Maven installed in your Jenkins instance
                    // Run Maven to build the project and generate the Jacoco report
                    bat 'mvn clean verify' // Use bat for Windows
                }
            }
        }

        stage('Jacoco Code Coverage') {
            steps {
                script {
                    // Run the Jacoco report generation
                    bat 'mvn jacoco:report' // Use bat for Windows

                    // Publish the Jacoco report in Jenkins
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
