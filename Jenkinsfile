pipeline {
    agent any

    tools {         // Use the tool names you configured in Jenkins
        maven 'Maven'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Yoganand30/guavaapp.git'
            }
        }

        stage('Build Project') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run Application') {
            steps {
                sh 'mvn exec:java -Dexec.mainClass="com.example.App"'
            }
        }
    }

    post {
        success {
            echo '✅ Build and execution successful!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
