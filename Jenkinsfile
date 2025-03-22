pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'manav771177@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application successfully... npm and maven can be used for build'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests... JUnit can be used for tests'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis... soanrQube and ESlint can be used for code ananlysis'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan... Bandit can be used for security scan'
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
                echo 'Deploying to staging environment... AWS and Docker can be used in Deploy'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging... Cypress can be used for integration'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production server... Heroku could be used for this deployment'
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
