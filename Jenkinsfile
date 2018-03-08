def projectName="JenkinsRepo From GitHub"


node {
   def mvnHome
   stage('SourceCodePull') { // for display purposes
      echo "Getting Source Code from GitHub for " + projectName
      // Get some code from a GitHub repository
      git 'https://github.com/rkpapineni/JenkinsRepo.git/'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
      echo "Source Code Pull from GitHub is complete."
   }
   stage('Build') {
       echo "Building Proect " + projectName
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
      echo "Build Complete."
   }
   stage('Results') {
       echo "Running Junit tests for project " + projectName
      //junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
      echo "Junit tests are complete."
   }
   stage('CodeQuality') {
       echo "Running SonarQube Code Quality tests for project " + projectName
       ///usr/local/bin/sonar-runner -e -Dsonar.host.url=env.SONAR_HOST_URL
      echo "Code Quality testing using SonarQube are complete."
   }
}
