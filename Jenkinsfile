pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    
    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
        // Uncomment the line below to use DockerHub credentials if needed
        // DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
    }
    
    stages {
        stage("Performing Build") {
            steps {
                script {
                    sh 'mvn -version'
                    sh 'mvn clean package'
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sa-sonar-scanner'
                }
            steps {
                script {
                    withSonarQubeEnv('sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}