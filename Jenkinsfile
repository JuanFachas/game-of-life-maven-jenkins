pipeline {
    agent any

    tools {
        // Ajusta los nombres a los que tengas en "Global Tool Configuration"
        maven 'Maven3-latest'
        jdk 'JDK17'
    }

    environment {
        // Opcionalmente puedes pasar opciones extra a Maven
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=false"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn -B clean verify'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn -B package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completado con éxito.'
        }
        failure {
            echo '❌ El build falló.'
        }
    }
}
