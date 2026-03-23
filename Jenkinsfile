pipeline {
    agent any

    tools {
        jdk 'JDK17'       // Jenkins me jo naam diya tha
        maven 'Maven3'    // Jenkins me jo naam diya tha
    }

    stages {

        stage('Checkout') {
            steps {
                // GitHub se code pull karega
                git branch: 'main',
                    url: 'https://github.com/tera-username/tera-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
            post {
                always {
                    // Test results publish karega
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Pipeline SUCCESS!'
        }
        failure {
            echo 'Pipeline FAILED!'
        }
    }
}
