
node('Maven-label') {

   def mvnHome

   stage('Preparation') { // for display purposes

      // Get some code from a GitHub repository

      git 'https://github.com/pramukhorg/shopping-app'

      // Get the Maven tool.

      // ** NOTE: This 'M3' Maven tool must be configured

      // **       in the global configuration.           

      mvnHome = tool 'Maven'

   }

   stage('Build') {

      // Run the maven build

      withEnv(["MVN_HOME=$mvnHome"]) {

         if (isUnix()) {

            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean install'

         } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

         }

      }

   }

   stage('Results') {

      junit '**/target/surefire-reports/TEST-*.xml'

      archiveArtifacts 'target/*.jar'

   }

}
