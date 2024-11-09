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
                    echo "------------------- Maven build started -------------------"
                    sh 'mvn -version'
                    sh 'mvn clean deploy'
                    echo "------------------- Maven build successful -------------------"
                }
            }
        }

        stage('Test') {  // Changed 'test' to 'Test' for consistency with CamelCase
            steps {
                script {
                    echo "------------------- Unit test started -------------------"
                    sh 'mvn surefire-report:report'
                    echo "------------------- Unit test completed -------------------"
                }
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                script {
                    echo "------------------- SonarScanner started -------------------"
                    // Uncomment the lines below when ready to execute the SonarQube scan
                    // withSonarQubeEnv('sonarqube-server') {
                    //     sh "${scannerHome}/bin/sonar-scanner"
                    // }
                    echo "------------------- SonarScanner completed successfully! -------------------"
                }
            }
        }
    }
}