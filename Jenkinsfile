pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo '📥 Code checkout ho raha hai...'
                checkout scm
            }
        }

        stage('Compile') {
            steps {
                echo '⚙️ Java code compile ho raha hai...'
                sh 'javac Driver.java'
                echo '✅ Compile successful!'
            }
        }

        // --- YEH STAGE ADD KAREIN ---
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Tool name wahi jo aapne 'sonar-scanner' rakha hai
                    def scannerHome = tool 'sonar-scanner'
                    
                    // Server name jo Jenkins System Settings mein hai
                    withSonarQubeEnv('sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=pizza-bill-calculator \
                        -Dsonar.projectName='Pizza Bill Calculator' \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=."
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '🐳 Docker image build ho rahi hai...'
                sh 'docker build --no-cache -t pizza-app .'
            }
        }

        stage('Run & Output') {
            steps {
                echo '🚀 Container run ho raha hai...'
                // Aapka current docker run command
                sh 'docker run --name pizza-container pizza-app || true'
            }
            post {
                always {
                    sh 'docker rm -f pizza-container || true'
                }
            }
        }
    }
}
