pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'pytest test_calculator.py'
            }
        }

        stage('Package') {
            steps {
                sh 'python3 setup.py bdist_wheel'
            }
        }
    }
}
