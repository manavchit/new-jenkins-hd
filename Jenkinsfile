pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'manav771177@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application successfully...'
                echo 'mvn clean package' // Use Maven as a build tool
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                echo 'mvn sonar:sonar' // Uses SonarQube for code analysis
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                echo 'mvn dependency-check:check' // OWASP Dependency Check
            }
            post {
                always {
                    emailext(
                        subject: 'Jenkins Security Scan Results',
                        body: 'Security scan completed. Check the logs for details.',
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                echo 'scp target/*.war user@staging-server:/path/to/deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'curl -X GET http://staging-server/api/health-check'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server...'
                echo 'scp target/*.war user@production-server:/path/to/deploy'
            }
        }
    }

   post {
         success {
             emailext subject: "Pipeline '${currentBuild.fullDisplayName}' Successful",
                       body: 'The build was successful. Congratulations!',
                       to: "${EMAIL_RECIPIENT}",
                       attachLog: true
         }
          failure {
             emailext subject: "Pipeline '${currentBuild.fullDisplayName}' Failed",
                       body: 'The build has failed. please investigate',
                       to: "${EMAIL_RECIPIENT}",
                       attachLog: true
         }
     }
}
