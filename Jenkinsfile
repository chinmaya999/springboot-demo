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
                sh '''
                # Stop previous instance if running
                pkill -f springboot-demo-0.0.1-SNAPSHOT.jar || true

                # Run the new JAR in the background
                nohup java -jar target/springboot-demo-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
                '''
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

