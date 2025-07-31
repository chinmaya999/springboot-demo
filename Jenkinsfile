pipeline {
    agent any

    environment {
        MAVEN_HOME = '/usr/share/maven'
    }

    stages {
        stage('Clone') {
            steps {
                echo "Cloning source code from GitHub..."
                // If using webhook, Jenkins auto clones
            }
        }

        stage('Build') {
            steps {
                echo "Building the Spring Boot app with Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'mvn test'
            }
        }

        stage('Archive') {
            steps {
                echo "Archiving the JAR file..."
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying application..."
                // Example: Copy JAR to remote server or run locally
                // sh 'scp target/*.jar user@server:/opt/app/'
                // Or run the app (optional)
                // sh 'java -jar target/*.jar &'
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}

