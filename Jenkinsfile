pipeline {
    agent {
        node {
            label 'maven'
        } 
    }
    environment{
         PATH ="/opt/apache-maven-3.9.9/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                // Build the project
                sh 'mvn clean package'
            }
        }
        
        stage('Test') {
            steps {
                // Run tests
                sh 'mvn test'
            }
        }
        stage('SonarQube analysis') {
            environment{
                scannerHome = tool 'sonar-scanner'
            }
           steps{  
            withSonarQubeEnv('sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
            sh "${scannerHome}/bin/sonar-scanner"
            }
         }
        }
        // Optional Deploy Stage can be removed if not needed
        /*
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
        */
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }

}