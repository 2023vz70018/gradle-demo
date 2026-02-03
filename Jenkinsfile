pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Set Gradle Wrapper Executable') {
            steps {
                sh 'chmod +x gradlew'
            }
        }

        stage('Build & Test') {
            steps {
                // Use Gradle wrapper (gradlew) in your repo
                sh './gradlew clean build test jacocoTestReport'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml'
        }
    }
}
