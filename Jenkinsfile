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
                sh 'mvn clean install'
            }
        }
        
        // stage('Test') {
        //     steps {
        //         // Run tests
        //         sh 'mvn test'
        //     }
        // }
        stage('SonarQube analysis') {
            environment{
               SONAR_HOST_URL = 'https://sonarcloud.io/' // Name of the SonarQube server configured in Jenkins
               SONARQUBE_TOKEN = 'cd4f8464b5fbc728783196718021d97ea4bc6060' // Token stored in Jenkins credentials
                
                scannerHome = tool 'galaxy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    // sh "${scannerHome}/bin/sonar-scanner -X"
                    sh 'mvn sonar:sonar -Dsonar.projectKey=valaxy47-key_twittertrend -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.login=$SONAR_AUTH_TOKEN'
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
        always {
            echo 'Pipeline Finished'
        }
    }


    //  post {
    //     success {
    //         echo 'Build and tests succeeded!'
    //     }
    //     failure {
    //         echo 'Build or tests failed!'
    //     }
    // }

}
