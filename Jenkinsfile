pipeline {
    agent any 
    tools {
        maven 'MAVEN3'
    }
    triggers {
        cron('H/10 * * * 1')
    }
    stages {
        stage('Build') {
            steps {
                script {
                    bat 'mvn clean package'
                }
            }
        }
        stage('Code Coverage') {
            steps {
                script {
                    bat 'mvn jacoco:report'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/jacoco/jacoco.xml', allowEmptyArchive: true
        }
    }
}
