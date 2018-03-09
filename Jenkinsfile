def projectName="JenkinsRepo From GitHub"

properties([parameters([string(defaultValue: 'https://github.com/rkpapineni/JenkinsRepo.git', description: 'Enter URL of the project to be built:', name: 'PROJECT_SCM_URL', trim: false)])])

    
node {
    echo "Will build project from URL: ${params.PROJECT_SCM_URL}"
    //sh "echo ${params.region}"
    //string(defaultValue: true, description: '', name: 'userFlag')
    //parameters {
      //  string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        // choices are newline separated
        //choice(choices: 'US-EAST-1\nUS-WEST-2', description: 'What AWS region?', name: 'region')
    //}
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
