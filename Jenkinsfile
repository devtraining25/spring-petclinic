node {
   def mvnHome

   
	
   stage('Checkout') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/devtraining25/spring-petclinic'
      // Get the Maven tool.
      // ** NOTE: This 'Maven3.6.3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven 3.6.3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {

      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
  }
  stage ('Docker Image: Build')
{
	 bat 'docker build -t catherinadoherty25/collegeproject:latest .'
	}
  stage('Push to Docker Image'){
    withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) { 
  bat "docker login -u catherinadoherty25 -p ${dockerHubPwd}"
}
bat 'docker push catherinadoherty25/collegeproject:latest'
}       
        stage('Run Container')
{def dockerRun='docker run -p 8081:8080 catherinadoherty25/collegeproject'
sshagent(['dev-server']) {
    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.35.157 ${dockerRun}"}
	}
}
