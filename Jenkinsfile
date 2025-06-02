pipeline {
    agent any

    environment {
        ANDROID_HOME = "/home/ubuntu/android-sdk"
        PATH+ANDROID = "${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools"
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
                    echo "✅ Environment PATH:"
                    echo "$PATH"
                    if [ -f ./gradlew ]; then
                        chmod +x ./gradlew
                    else
                        echo "❌ gradlew file not found"
                        exit 1
                    fi
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
