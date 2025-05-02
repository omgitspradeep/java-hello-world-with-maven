pipeline {
    agent none
    stages {

        stage('Back-end Build') {
            agent {
                docker {  image 'maven:3.8.1-adoptopenjdk-11' }
            }

            steps {
                sh 'mvn --version'
                sh 'mvn clean install -DskipTests'  // Basic build with test skipping
                
                // Alternative for full build (with tests)
                // sh 'mvn clean install'
                
                // Store build artifacts
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }

            post {
                success {
                    echo 'Build successful! Artifacts archived.'
                }
                failure {
                    echo 'Build failed! Check logs for details.'
                }
            }

            
        }
    }


    post {
        always {
            echo 'Pipeline completed - sending notifications'
            // Add email/chat notification here if needed
        }
    }



}
