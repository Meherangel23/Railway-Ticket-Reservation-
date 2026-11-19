pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Downloading Railway Reservation source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Starting application build'
                sh '''
                    test -f index.html || exit 1
                    test -f style.css || exit 1
                    test -f script.js || exit 1
                    echo "Application files verified successfully"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application files'
                grep -i "<html" index.html
                grep -i "bookingForm" index.html
                grep -i "addEventListener" script.js
                echo "All basic validation tests passed"
            }
        }

        stage('Package') {
            steps {
                echo 'Creating application package'
                rm -f railway-reservation.zip
                zip railway-reservation.zip index.html style.css script.js
            }
        }
    }

    post {
        success {
            echo 'Railway Reservation Build Successful!'