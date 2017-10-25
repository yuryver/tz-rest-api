pipeline {
    agent any
    
    stages {
        stage('Commit') {
            steps {
                sh './gradlew clean assemble'
            }
        }
        
        stage('CodeQuality') {
            steps {
                sh './gradlew sonarqube -Dsonar.host.url=http://sonarqube:9000'
                sh './gradlew jacocoTestReport'
                publishHTML target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'build/jacocoHtml/',
                    reportFiles: 'index.html',
                    reportName: 'Code Coverage Report'
                ]
            }
        }

        
    }

    post {
        always {
            junit 'build/test-results/test/*'
        }
    }
}