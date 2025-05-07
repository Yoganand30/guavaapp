pipeline {
    agent any

    tools {
        maven 'maven-3.8.8'  // Change to your actual Maven tool name
        jdk 'jdk8'           // Change to your configured JDK name
    }

    environment {
        APP_JAR = "target/MyMavenGuavaApp-1.0-SNAPSHOT-shaded.jar"
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
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Run App') {
            steps {
                script {
                    if (fileExists(env.APP_JAR)) {
                        echo "Running application JAR: ${env.APP_JAR}"
                        sh "java -jar ${env.APP_JAR}"
                    } else {
                        echo "Available JARs:"
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
