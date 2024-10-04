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
                echo ".............build started..."
                // Build the project
                sh 'mvn clean install -Dmaven.test.skip=true'
                echo "..........build completed............"
            }
        }
        stage('Test'){
            steps{
                echo "............unit test started.........."
                sh 'mvn surefire-report:report'
                echo"..........unit test completed......."
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
                scannerHome = tool 'galaxy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner -X \
                        -Dsonar.projectKey=valaxy47-key_twittertrend\
                        -Dsonar.organization=valaxy47-key  \
                        -Dsonar.login=cd4f8464b5fbc728783196718021d97ea4bc6060 \
                        -Dsonar.java.binaries=target/classes"
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