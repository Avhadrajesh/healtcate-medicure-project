pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage("Performing build"){
            steps {
                sh 'mvn clean deploy'
            }
        }    
    }
}

    
        