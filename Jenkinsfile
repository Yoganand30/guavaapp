pipeline {
    agent any

    tools {
        maven 'Maven'  // Change to your actual Maven tool name
    // Change to your configured JDK name
    }

    environment {
        APP_JAR = "target/MyMavenGuavaApp-1.0-SNAPSHOT.jar"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean install -DskipTests'  // Install all dependencies and skip tests
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'  // Run tests after build
            }
        }

        stage('Run App') {
            steps {
                script {
                    if (fileExists(env.APP_JAR)) {
                        echo "Running application JAR: ${env.APP_JAR}"
                        sh "java -jar ${env.APP_JAR}"
                    } else {
                        echo "No JAR found in target directory."
                        sh 'ls -lh target/*.jar || echo "No JARs found."'
                        error "JAR file not found: ${env.APP_JAR}"
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and run successful!'
        }
        failure {
            echo '❌ Build failed or JAR missing.'
        }
    }
}
