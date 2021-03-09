pipeline {
    agent any

    stages {
        stage ('PetClinic - Build') {
                steps {
                sh "mvn package " 
            }
        	// JUnit Results
		junit '**/target/surefire-reports/*.xml' 
	}
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
