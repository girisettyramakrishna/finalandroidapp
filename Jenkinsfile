pipeline {
    agent any

    environment {
        ANDROID_HOME = "/home/ubuntu/android-sdk"
        PATH = "${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/girisettyramakrishna/finalandroidapp.git', branch: 'master'
            }
        }

        stage('Prepare SDK & Permissions') {
            steps {
                sh '''
                    echo "PATH: $PATH"
                    chmod +x ./gradlew || echo "gradlew not found"
                '''
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
        success {
            echo "✅ Build succeeded!"
        }
        failure {
            echo "❌ Build failed!"
        }
    }
}
