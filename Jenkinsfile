pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
        jdk 'jdk21'
    }

    stages {

        stage('Checkout') {
            steps {
                echo "========================================"
                echo "Stage 1: Checking out source code..."
                echo "========================================"

                git branch: 'main',
                    url: 'https://github.com/Keerthivasan31/maven.git'

                echo "✅ Source code checkout completed."
            }
        }

        stage('Build') {
            steps {
                echo "========================================"
                echo "Stage 2: Compiling Maven Project..."
                echo "========================================"

                sh 'mvn clean compile'

                echo "✅ Build completed successfully."
            }
        }

        stage('Test') {
            steps {
                echo "========================================"
                echo "Stage 3: Running Unit Tests..."
                echo "========================================"

                sh 'mvn test'

                echo "✅ All tests executed."
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    echo "📊 Test report published."
                }
            }
        }

        stage('Package') {
            steps {
                echo "========================================"
                echo "Stage 4: Packaging Application..."
                echo "========================================"

                sh 'mvn package'

                echo "✅ JAR package created."
            }
        }

        stage('Archive') {
            steps {
                echo "========================================"
                echo "Stage 5: Archiving Build Artifact..."
                echo "========================================"

                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true

                echo "✅ Artifact archived successfully."
            }
        }
    }

    post {
        success {
            echo "========================================"
            echo "🎉 BUILD SUCCESSFUL"
            echo "Maven project built successfully."
            echo "Artifact archived in Jenkins."
            echo "========================================"
        }

        failure {
            echo "========================================"
            echo "❌ BUILD FAILED"
            echo "Check the console log for the error."
            echo "========================================"
        }

        always {
            echo "========================================"
            echo "Pipeline execution finished."
            echo "========================================"
        }
    }
}
