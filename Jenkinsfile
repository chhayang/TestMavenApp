node {
   def mvnHome
   stage('Get Code from GIT') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/chhayang/TestMavenApp.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Generated Artifacts') {
    
      archiveArtifacts 'target/*.war'
   }
   
   stage('Deployment on Destination Server') {
    
    sh label: '', script: '''sleep 10s
                            pwd
                            sudo /Users/tu455sq/Documents/Scripts/deploy.sh
    '''
      
   }
   
   stage('Send Email After Completion'){ 
   emailext body: '$DEFAULT_CONTENT', subject: '$DEFAULT_SUBJECT', to: 'chhayang.patel@ey.com'
   }
}
