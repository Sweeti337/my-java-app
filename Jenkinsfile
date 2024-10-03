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
        
        stage('Deploy') {
            steps {
                // Example deployment step (just echoing here)
                echo 'Deploying application...'
                // You can add your deployment logic here
            }
        }
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
