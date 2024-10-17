pipeline {
    agent any 

    triggers {
        cron('H */10 * * 1')
    }

    stages {

        stage('Build and Test') {
            steps {
                script {
                    bat 'mvn clean verify'
                }
            }
        }

        stage('Jacoco Code Coverage') {
            steps {
                script {
                    bat 'mvn jacoco:report'
                    
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
            cleanWs()
        }
    }
}
