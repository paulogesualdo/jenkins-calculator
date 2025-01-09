pipeline {
    agent any

    stages {
        stage('Check operation') {
            steps {
                echo 'Checking if the operation was passed as parameter'
            }
        }

        stage('Show current total') {
            steps {
                echo 'The current total is: XXXX'
            }
        }

        stage('Input value') {
            steps {
                echo 'Please type the value: XXXX'
            }
        }

        stage('Call calculador pipeline') {
            steps {
                echo 'Calling calculator pipeline'
            }
        }
        
        stage('Show the new value') {
            steps {
                echo 'The new value is: XXXX'
            }
        }
    }
}