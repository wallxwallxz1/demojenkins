pipeline {
   agent any
    environment{
       OKTA_OAUTH2_ISSUER         = '{https://dev-709745.okta.com}/oauth2/default'
       OKTA_OAUTH2_CLIENT_ID      =  credentials('0oad10fp4SrzJxZD04x6')
       OKTA_OAUTH2_CLIENT_SECRET  =  credentials('Tb_wVhqIU6VMEvoKU2Rj3XK81vUqJcJe3Wq6D6N8')
   }
   stages {
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/wallxwallxz1/demojenkins.git'

            // Run Maven on a Unix agent.
            sh "./mvnw -Dmaven.test.failure.ignore=true clean package"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
   }
}
