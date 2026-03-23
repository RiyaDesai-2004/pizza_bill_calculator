pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'javac Driver.java'
            }
        }

        stage('Run') {
            steps {
                echo 'Running the project...'
                sh 'java Driver'
            }
        }

    }

    post {
        success {
            echo 'Pipeline SUCCESS! ✅'
        }
        failure {
            echo 'Pipeline FAILED! ❌'
        }
    }
}
