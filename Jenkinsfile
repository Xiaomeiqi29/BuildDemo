pipeline {
    agent any

    tools {
        jdk 'JDK11'
        gradle 'Gradle8'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Xiaomeiqi29/BuildDemo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean assembleDebug'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: '**/build/outputs/**/*.apk', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully.'
        }

        failure {
            echo 'Build failed.'
        }
    }
}
