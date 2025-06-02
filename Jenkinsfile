pipeline {
    agent any

    environment {
        ANDROID_HOME = '/home/ubuntu/android-sdk'
        // Use Jenkins-specific syntax to extend PATH
        PATH = "${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
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
                    echo "sdk.dir=${ANDROID_HOME}" > local.properties
                    chmod +x ./gradlew
                '''
            }
        }

        stage('Build APK') {
            steps {
                sh './gradlew clean assembleDebug'
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
            echo '✅ Build succeeded!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
