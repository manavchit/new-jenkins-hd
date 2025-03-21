pipeline{
  agent any

  stages{
    stage("Hello"){
      steps{
      echo "Hi shh"  
      }
    }
  }
    post {
         success {
             emailext subject: "Pipeline '${currentBuild.fullDisplayName}' Successful",
                       body: 'The build was successful. Congratulations!',
                       to: 'manav771177@gmail.com',
                       attachLog: true
         }
          failure {
             emailext subject: "Pipeline '${currentBuild.fullDisplayName}' Failed",
                       body: 'The build has failed. please investigate',
                       to: 'manav771177@gmail.com',
                       attachLog: true

}
    }
