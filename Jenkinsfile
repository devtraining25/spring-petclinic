pipeline {
    agent any

    stages {
        stage ('PetClinic - Build') {
                steps {
                sh "mvn package " 
            }
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
