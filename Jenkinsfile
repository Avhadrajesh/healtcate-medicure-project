pipeline {
    agent {
        node {
            label 'maven' // Ensuring the pipeline runs on a node labeled 'maven'
        }
    }
    
    environment {
        // Ensure Maven is in the PATH
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
        // Use credentials stored in Jenkins for DockerHub
        DOCKERHUB_CREDENTIALS = credentials('dockerlogin')
    }
    
    stages {
        stage("Performing Build") {
            steps {
                script {
                    // Print the Maven version to verify installation
                    sh 'mvn -version'

                    // Perform Maven build
                    sh 'mvn clean package'
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    echo 'Performing Docker Build'
                    sh "docker build -t rajesh4ever/banking-finance:${BUILD_NUMBER} ."
                    sh "docker tag rajesh4ever/banking-finance:${BUILD_NUMBER} rajesh4ever/banking-finance:latest"
                    sh 'docker image list'
                }
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
