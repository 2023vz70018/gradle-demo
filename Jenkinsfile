pipeline {
    agent any

    tools {
        jdk 'JDK17'   // Replace with your configured JDK in Jenkins
        gradle 'Gradle' // Replace with your configured Gradle in Jenkins
    }

    environment {
        // If SonarQube requires a token, configure it as a Jenkins secret and reference it
        SONAR_HOST_URL = 'http://localhost:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh './gradlew clean build jacocoTestReport'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Run SonarQube via Gradle plugin, not CLI
                    sh './gradlew sonarqube'
                }
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
