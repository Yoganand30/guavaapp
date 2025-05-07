pipeline {
    agent any

    tools {
        maven 'Maven'    // Use your Maven tool name in Jenkins        // Use your configured JDK
    }

    environment {
        APP_JAR = "target/MyMavenGuavaApp-1.0-SNAPSHOT-shaded.jar"
    }

    stages {
        stage('Checkout') {
            steps {
                // If you're using Git, Jenkins will automatically check out the source
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Run App') {
            steps {
                script {
                    if (fileExists(env.APP_JAR)) {
                        sh "java -jar ${env.APP_JAR}"
                    } else {
                        error "JAR file not found: ${env.APP_JAR}"
                    }
                }
            }
        }

        // Optional: stage to push code back to Git or deploy artifact
        // stage('Deploy') {
        //     steps {
        //         echo 'Deploying application or pushing artifacts...'
        //     }
        // }
    }

    post {
        success {
            echo 'Build and run successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
