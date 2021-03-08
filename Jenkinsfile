pipeline {
    agent any

    stages stage ('PetClinic - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/devtraining25/spring-petclinic']]]) 
	}
	stage ('PetClinic - Build') {
 			// Maven build step
	withMaven(maven: 'Maven 3.6.3') { 
 			if(isUnix()) {
 				sh "mvn package " 
			} else { 
 				bat "mvn package " 
			} 
 		}
		// JUnit Results
		junit '**/target/surefire-reports/*.xml' 
	}
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
