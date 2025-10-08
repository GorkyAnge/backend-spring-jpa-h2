pipeline {
    agent any
    
    tools {
        maven 'Maven'
        jdk 'JDK'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn clean test'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn package -DskipTests'
            }
        }
    }
    
    post {
        success {
            echo 'Archiving artifacts...'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
