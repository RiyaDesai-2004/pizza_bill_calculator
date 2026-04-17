pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'javac Driver.java'
            }
        }

        // --- SonarQube Stage Start ---
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Yahan 'sonar-scanner' likhna hai kyunki aapne ye naam rakha hai
                    def scannerHome = tool 'sonar-scanner' 
                    
                    // Server ka naam (jo Manage Jenkins > System mein rakha tha)
                    withSonarQubeEnv('sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=pizza-bill-calculator \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=."
                    }
                }
            }
        }
        // --- SonarQube Stage End ---

        stage('Check Class File') {
            steps {
                echo 'Checking compiled output...'
                sh 'ls -la *.class'
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
