pipeline {
    agent any

    tools {
        jdk 'JDK17'
        gradle 'Gradle8'
    }

     environment {
        ANDROID_HOME = '/Users/meiqi.xiao/Library/Android/sdk'
        PATH = "${ANDROID_HOME}/platform-tools:${PATH}"
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
