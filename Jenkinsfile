pipeline {
    agent any

    tools {
        jdk 'JDK17'
        gradle 'Gradle8'
    }

    environment {
        JAVA_HOME = '/opt/java/openjdk'
        ANDROID_HOME = '/opt/android-sdk'
        PATH = "$JAVA_HOME/bin:$PATH"
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
