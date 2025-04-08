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

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Xiaomeiqi29/BuildDemo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo "🛠️ 正在构建 APK..."
                sh './gradlew clean assembleDebug'
            }
        }

        stage('Test') {
            steps {
                echo "🧪 正在运行测试..."
                sh './gradlew testDebugUnitTest'
            }
        }

        stage('Archive APK') {
            steps {
                echo "📦 正在归档 APK..."
                archiveArtifacts artifacts: '**/build/outputs/**/*.apk', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully.'
        }

        failure {
            echo '❌ Build failed. Please check the logs.'
        }
    }
}
