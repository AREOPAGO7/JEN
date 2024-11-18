pipeline {
    agent any
    environment {
        SONARQUBE = 'SonarQube' // SonarQube server name in Jenkins
        SONAR_TOKEN = 'sqp_a801f03d349994f2882a780cece76ada1364f24b' // Hardcoded token (not recommended for production)
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube analysis with hardcoded token
                    sh """
                        mvn sonar:sonar \
                            -Dsonar.projectKey=my_project_key \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=${env.SONAR_TOKEN}
                    """
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
