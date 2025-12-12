pipeline {
    agent any
    tools {
        // This name must match exactly what you set in 'Global Tool Configuration'
        maven 'MyMaven' 
    }
    stages {
        stage('Checkout') {
            steps {
                // Jenkins does this automatically for "Pipeline from SCM", 
                // but it's good to know this stage exists implicitly.
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn clean install' // For Mac/Linux
                    } else {
                        bat 'mvn clean install' // For Windows
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                // Maven 'install' already runs tests, but here is how you'd run them separately
                script {
                    if (isUnix()) {
                        sh 'mvn test'
                    } else {
                        bat 'mvn test'
                    }
                }
            }
        }
        stage('Run JAR') {
            steps {
                echo 'Running the JAR file...'
                script {
                    if (isUnix()) {
                        sh 'java -cp target/my-app-1.0-SNAPSHOT.jar com.example.App'
                    } else {
                        bat 'java -cp target\\my-app-1.0-SNAPSHOT.jar com.example.App'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}