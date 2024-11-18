pipeline {
    agent any

    environment {
        SONARQUBE = 'sonarserver'  // Use the name configured earlier
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Add your build commands here (e.g., for Maven, Gradle, or npm)
                sh 'mvn clean install'  // Example for Maven
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Trigger the SonarQube scan
                    def scannerHome = tool 'SonarQube Scanner'
                    withSonarQubeEnv(SONARQUBE) {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    // Wait for the analysis to complete and check the Quality Gate status
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
