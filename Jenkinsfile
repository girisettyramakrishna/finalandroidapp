pipeline {
    agent any
    environment {
        ANDROID_HOME = "/home/ubuntu/android-sdk"
        PATH+ANDROID = "${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"
    }
    stages {
        stage('Prepare SDK & Permissions') {
            steps {
                sh 'echo "PATH: $PATH"'
                sh 'chmod +x gradlew'
            }
        }
        stage('Build APK') {
            steps {
                sh './gradlew assembleDebug'
            }
        }
        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: '**/app/build/outputs/apk/debug/*.apk', fingerprint: true
            }
        }
    }
    post {
        failure {
            echo "❌ Build failed!"
        }
        success {
            echo "✅ Build succeeded!"
        }
    }
}
