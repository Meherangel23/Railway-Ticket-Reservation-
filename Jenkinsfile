pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Validating application files..."
                    test -f index.html
                    test -f style.css
                    test -f script.js
                    echo "All application files found"
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    echo "Testing file contents..."
                    grep -qi "<html" index.html
                    grep -q "bookingForm" index.html
                    grep -q "addEventListener" script.js
                    echo "All content checks passed"
                '''
            }
        }

        stage('Package') {
            steps {
                sh '''
                    rm -f railway-reservation.zip
                    zip railway-reservation.zip index.html style.css script.js
                    ls -l railway-reservation.zip
                '''
            }
        }
    }
}
