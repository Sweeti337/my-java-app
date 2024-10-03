pipeline {
    agent any 

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
